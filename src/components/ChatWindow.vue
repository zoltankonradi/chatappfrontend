<template>
    <div id="messageArea" class="row windowHide">
        <div class="col-md-4">
            <div class="well">
                <h3>Online users({{ this.users.length }})</h3>
                <ul class="list-group" id="users">
                    <li v-for="user in users" :key="user.userId">{{ user.userName }}</li>
                </ul>
            </div>
        </div>
        <div class="col-md-8">
            <div class="chat" id="chat">
                <div v-for="msg in messages" :key="msg.msgId" class="messages">{{ msg.user }}: {{ msg.messageText }}</div>
            </div>
            <form id="messageForm">
                <div class="form-group">
                    <label for="message">Enter message</label>
                    <textarea v-model="message" class="form-control" id="message"></textarea>
                    <br>
                    <button v-on:click="sendMessage" class="btn btn-primary" type="button">Send Message</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    const socket = io.connect(process.env.PORT ||'http://localhost:8081/');
    import io from 'socket.io-client';
    export default {
        name: "ChatWindow",
        mounted() {
            this.$root.$on('showChatWindow', (userName) => {
                const chatWindow = document.getElementById('messageArea');
                this.openConnection(userName, chatWindow);
            });
            socket.on('new message', (data) => {
                this.addNewMessage(data);
            });
            socket.on('get users', (data) => {
                this.addNewUser(data);
            });
        },
        methods: {
            openConnection(userName, chatWindow) {
                socket.emit('new user', userName, (data) => {
                    if (data) {
                        chatWindow.classList.remove('windowHide');
                        chatWindow.classList.add('windowShow');
                    }
                })
            },
            sendMessage() {
                socket.emit('send message', this.message);
                this.message = null;
            },
            addNewMessage(data) {
                this.messages.push({
                    msgId: ++this.counter,
                    messageText: data.message,
                    user: data.user
                })
            },
            addNewUser(data) {
                this.users = [];
                for (let user of data) {
                    this.users.push({
                        userId: ++this.userCounter,
                        userName: user
                    });
                }
            }
        },
        data() {
            return {
                counter: 0,
                userCounter: 0,
                message: null,
                messages: [],
                users: []
            }
        }
    }
</script>

<style scoped>
    .windowShow {
        display: block;
    }
    .windowHide {
        display: none;
    }
</style>
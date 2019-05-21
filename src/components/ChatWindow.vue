<template>
    <div id="messageArea" class="row windowHide">
        <div class="col-md-4">
            <div class="well">
                <h3>Online users</h3>
                <ul class="list-group" id="users"></ul>
            </div>
        </div>
        <div class="col-md-8">
            <div class="chat" id="chat"></div>
            <form id="messageForm">
                <div class="form-group">
                    <label>Enter message</label>
                    <textarea class="form-control" id="message"></textarea>
                    <br>
                    <button v-on:click="sendMessage" class="btn btn-primary" type="button">Send Message</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    import io from 'socket.io-client';
    export default {
        name: "ChatWindow",
        mounted() {
            this.$root.$on('showChatWindow', (userName) => {
                // this.userName = userName;
                const chatWindow = document.getElementById('messageArea');
                this.openConnection(userName, chatWindow);
            })
        },
        methods: {
            openConnection(userName, chatWindow) {
                const socket = io.connect('http://localhost:8081/');
                socket.emit('new user', userName, (data) => {
                    console.log(userName);
                    if (data) {
                        chatWindow.classList.remove('windowHide');
                        chatWindow.classList.add('windowShow');
                        console.log(data + " from server");
                    }
                })
            },
            sendMessage() {

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
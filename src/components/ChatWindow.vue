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
                    <input type="submit" class="btn btn-primary" value="Send Message"/>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ChatWindow",
        mounted() {
            this.$root.$on('showChatWindow', (userName) => {
                // this.userName = userName;
                const chatWindow = document.getElementById('messageArea');
                chatWindow.classList.remove('windowHide');
                chatWindow.classList.add('windowShow');
                console.log(userName + 'chatwindow');
            })
        },
        methods: {

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
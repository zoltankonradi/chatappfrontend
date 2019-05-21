<template>
    <div id="userFormArea" class="row">
        <div class="col-md-12">
            <form id="userForm">
                <div class="form-group">
                    <label for="username" >Enter Username</label>
                    <input v-model="userName" class="form-control" id="username">
                    <br>
                    <button v-on:click="hideRegistration" class="btn btn-primary" type="button">Login</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
        name: "UserRegistration",
        methods: {
            hideRegistration: function() {
                document.getElementById('userFormArea').classList.add('reghide');
                this.$root.$emit('showChatWindow', this.userName)
            }
        },
        data() {
            return {
                userName: null
            }
        }
    }
</script>

<style scoped>
    .reghide {
        display: none;
    }
</style>
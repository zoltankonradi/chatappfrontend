<template>
  <div id="app" class="container">
    <div id="title"><h1>{{title}}</h1></div>
    <UserRegistration />
    <ChatWindow />
  </div>
</template>

<script>
import UserRegistration from './components/UserRegistration';
import ChatWindow from './components/ChatWindow';
export default {
  name: 'app',
  components: {
    UserRegistration,
    ChatWindow
  },
  data() {
    return {
      title: 'Chat app'
    }
  }
}
</script>

<style>
/*#app {*/
/*  font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
/*  -webkit-font-smoothing: antialiased;*/
/*  -moz-osx-font-smoothing: grayscale;*/
/*  text-align: center;*/
/*  color: #2c3e50;*/
/*  margin-top: 60px;*/
/*}*/
</style>

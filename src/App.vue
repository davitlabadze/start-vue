<template>
  <div id="App">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">
          Blog
        </div>
      </router-link>
      
      <div class="navigation__user">
        {{ state.user.username }}
      </div>
    </nav>
   <!-- <UserProfile/> -->
   <router-view/>
  </div>
</template>

<script>
import { reactive } from 'vue';
// import UserProfile from "./components/UserProfile";
export default {
  name: 'App',
  // components : { UserProfile },
  setup(){
   const state = reactive({
     user:{
        username: 'vueMaster'
      }
    })
    return {
      state
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color:#2c3e50;
  min-height: 100vh;
  background-color: #3a5169;
  
  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: #42b983;
    color: white;
    .navigation__logo {
      font-weight: bold;
      font-size: 24px;
    }
    .navigation__user {
      font-weight: bold;
    }
  }
}
</style>
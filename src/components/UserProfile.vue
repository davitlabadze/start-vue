<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }} </h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      <button @click="followUser">Follow</button>
      </div>
    </div>
    <div class="user-profile__master-wrapper">
      <MasterItem 
      v-for="master in user.masters" 
      :key="master.id" 
      :username="user.username" 
      :master="master" 
      @favourite="toggleFavourite" />
    </div>
  </div>
</template>

<script>

import MasterItem from "./MasterItem";
export default {
  name: 'UserProfile',
  components : {MasterItem},
  data(){
    return{
      followers : 0,
      user: {
        id : 1,
        username : 'vueMaster',
        firstName : 'john',
        lastName : 'doe',
        email : 'vueMaster@gmail.com',
        isAdmin : true,
        masters: [
          { id: 1, content: 'vue start'},
          { id: 2, content: "hello vue"}
        ]
      }
    } 
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if (oldFollowerCount < newFollowerCount){
        console.log (`${this.user.username} has gained a follower!`)
      }
    }

  },
  computed :{
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUser(){
      this.followers++
    },
    toggleFavourite(id) {
      console.log(`Favourited Tweet #${id}`)
    }
  },
  mounted(){
    this.followUser();
  }
  
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.user-profile{
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding:50px 5%;
}

.user-profile__user-panel{
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3eb;
}
.user-profile__admin-badge{
  /* border: 1px solid #0fe368; */
  border-radius: 5px;
  margin-right: auto;
  background-color:green;
  color: #fff;
  padding: 0 10px;
  font-weight: bold;
  
}

h1{
  margin: 0;
}
</style>

<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }} </h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <CreatePostPanel @add-post="addPost"/> 
    </div>
    <div class="user-profile__posts-wrapper">
      <PostItem 
      v-for="post in user.posts" 
      :key="post.id" 
      :username="user.username" 
      :post="post" />
    </div>
  </div>
</template>

<script>

import PostItem from "./PostItem";
import CreatePostPanel from "./CreatePostPanel";
export default {
  name: 'UserProfile',
  components : { CreatePostPanel, PostItem},
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
        posts: [
          { id: 1, content: 'vue start'},
          { id: 2, content: "hello vue"}
        ]
      }
    } 
  },
  methods: {
    addPost(post){
      this.user.posts.unshift({ id: this.user.posts.length + 1, content: post });
    }
  }
};


</script>


<style lang="scss" scoped>
.user-profile {
  
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;
  .user-profile__user-panel {
    
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #82f01c;
    margin-bottom: auto;
    h1 {
      margin: 0;
    }
    .user-profile__admin-badge {
      background: green;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }
  .user-profile__posts-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}
</style>

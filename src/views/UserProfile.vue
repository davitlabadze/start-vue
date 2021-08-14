<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ state.user.username }} </h1>
        <div class="user-profile__admin-badge" v-if="state.user.isAdmin">
          Admin
        </div>
        <div class="user-profile__follower-count">
          <strong>Followers: </strong> {{ state.followers }}
        </div>
      </div>
      <CreatePostPanel @add-post="addPost"/> 
    </div>
    <div class="user-profile__posts-wrapper">
      <PostItem 
      v-for="post in state.user.posts" 
      :key="post.id" 
      :username="state.user.username" 
      :post="post" />
    </div>
  </div>
</template>

<script>
import { reactive, computed } from 'vue';
import { useRoute } from 'vue-router';
import { users } from "../assets/users";
import PostItem from "../components/PostItem.vue";
import CreatePostPanel from "../components/CreatePostPanel.vue";

export default {
  name: 'UserProfile',
  components : { CreatePostPanel, PostItem},

  setup(){

    const route = useRoute();
    const userId = computed(() => route.params.userId);

    //if(userId) fetchUserFromApi(userId)



    const state = reactive({
      followers : 0,
      user: users[userId.value -1] || users[0]
    });

    function addPost(post){
      state.user.posts.unshift({ id: state.user.posts.length + 1, content: post });
    }
    return {
      state,
      addPost,
      userId
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
    background-color: #1d2935;
    color:#fff;
    border-radius: 6px;
    border: 1px solid #42b983;
    margin-bottom: auto;
    h1 {
      margin: 0;
    }
    .user-profile__admin-badge {
      background: #42b983;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }
  .user-profile__posts-wrapper {
    display: grid;
    grid-gap: 20px;
    padding: 20px;
    margin-bottom: auto;
    background: #2c3e50;
    border-radius: 6px;
    
  }
}
</style>

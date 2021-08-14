<template>
    <form class="create-post-panel" @submit.prevent="createNewPost" :class="{ '--exceeded': newPostCharacterCount > 150 }">
        <label for="newPost"><strong>new Post</strong>({{ newPostCharacterCount }}/150) </label>
        <textarea placeholder="What's happening?" id="newpPost" rows="4" maxlength="150" v-model="state.newPostContent"/>

        <div class="create-post-panel__submit">
            <div class="create-post-type">
                <label for="newPostType"><strong>Type: </strong></label>
                <select name="" id="newPostType" v-model="state.selectedPostType">
                <option :value="option.value" v-for="(option,index) in state.postTypes" :key="index">
                    {{ option.name }}
                </option>
                </select>
            </div>
            <button>Post</button>
        </div>
        
    </form>
</template>

<script>
import {reactive, computed } from 'vue';


export default {
  name: 'CreatePostPanel',
  setup(props, ctx){
    const state = reactive({
      newPostContent: '',
      selectedPostType: 'instant',
      postTypes:[
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Post'}
      ]
    }) 


    const newPostCharacterCount = computed(() => state.newPostContent.length);

    function createNewPost() {
      if(state.newPostContent && state.selectedPostType !== 'draft'){
        ctx.emit('add-post', state.newPostContent);
        state.newPostContent = '';
      }
    }

  
    return {
      state,
      newPostCharacterCount,
      createNewPost
    }
  }
};

</script>


<style lang="scss" scoped>
.create-post-panel {
  background-color: #1d2935;
  border-radius: 6px;
  border:1px solid #42b983;
  color:#fff;
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  textarea {
    resize: none;
    background-color: #192024;
    border:none;
    color:#fff;
    border-radius: 5px;
    outline:none;

    &::placeholder{
      color:#42b983;
      opacity: 0.4;
    }
    &:focus{
      
      background-color:#1d2935;
    }
  }
  .create-post-panel__submit {
    display: flex;
    justify-content: space-between;
    .create-post-type {
      padding: 10px 0;
    }
    button {
      cursor: pointer;
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: #42b983;
      color: white;
      font-weight: bold;
    }

    option{
      background-color:blue;
      color:red;
    }
  }
  &.--exceeded {
    color: red;
    border-color: red;
    .create-post-panel__submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style>
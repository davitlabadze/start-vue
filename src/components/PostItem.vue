<template>
  <div class="post-item">
      <div class="user-profile__post">
          <div class="post-item__user">
              @{{ username }}
          </div>
          <div class="post-item__content">
              {{ post.content }}
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'PostItem',
  props: {
      username: {
          type: String,
          required: true,
        },
      post: {
          type: Object,
          required: true
        }
    }
};

</script>


<style lang="scss" scoped>
.post-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #82f01c;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  &:hover {
    background-color:green;
  }
  .post-item__user {
    font-weight: bold;
  }
}
</style>
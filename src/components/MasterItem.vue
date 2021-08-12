<template>
  <div class="master-item" @click="favouriteMaster(master.id)">
      <div class="user-profile__master">
          <div class="master-item__user">
              @{{ username }}
          </div>
          <div class="master-item__content">
              {{ master.content }}
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'MasterItem',
  props: {
      username: {
          type: String,
          required: true,
        },
      master: {
          type: Object,
          required: true
        }
    },
    methods:{
        favouriteMaster(id){
            this.$emit('favourite',id)
        }
    }
};

</script>


<style>

.master-item{
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    box-sizing: border-box;
    cursor: pointer;
    translate: all 0.25s ease;
}

.master-item:hover{
    transform: scale(1.1,1);
}

.master-item__user{
    font-weight: bold;
}
</style>

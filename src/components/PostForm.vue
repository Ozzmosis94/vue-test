<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <my-input v-model="post.title" type="text" placeholder="Название:" />

    <my-input v-model="post.body" classype="text " placeholder="Описание:" />
    <my-button class="btnss" @click="CreatePost">Создать</my-button>
  </form>
</template>

<script>
import MyButton from "./UI/MyButton.vue";
export default {
  components: { MyButton },
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    CreatePost() {
      this.post.id = Date.now();
      this.$emit("create", this.post);
      // this.post = {
      //   title: " ",
      //   body: " ", //очищение
      // };
    },
  },
  //  watch:{
  //   handler(newVal){
  //     console.log(newVal)
  //   },
  //   deep:true
  // }
};
</script>

<style>
form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 2px solid grey;
  padding: 10px 15px;
  margin-top: 15px;
}
.app {
  padding: 20px;
}
.btnss {
  display: flex;
  justify-content: flex-end;
  margin-top: 15px;
}
</style>

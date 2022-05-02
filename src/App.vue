<template>
  <div class="app">
    <h1 class="title">Страница с постами</h1>
    <my-input v-model="searchQuery" placeholder="Поиск..." />
    <div class="app__btns">
      <my-button @click="showDialog" class="title">Создать пост </my-button>
      <my-select v-model="selectedSord" :options="sortOptiops" />
    </div>

    <my-dialog v-model:show="dialodVisible">
      <PostForm @create="CreatePost" />
    </my-dialog>
    <PostList
      :posts="sorteAndSearchedPost"
      @remove="RemovePost"
      v-if="!isPostLoading"
    />
    <div v-else>Идет загрузка...</div>
    <div class="page__wrapper">
      <div
        v-for="pageNumber in TotalPages"
        :key="pageNumber"
        class="page"
        :class="{ 'current-page': page === pageNumber }"
      >
        {{ pageNumber }}
      </div>
    </div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from "axios";
import MyButton from "./components/UI/MyButton.vue";

export default {
  components: {
    PostForm,
    PostList,
    MyButton,
  },
  data() {
    return {
      posts: [
        //массив постов
      ],
      dialodVisible: false,
      isPostLoading: false,
      selectedSord: "",
      searchQuery: "",
      page: 1,
      limit: 10,
      TotalPages: 0,

      sortOptiops: [
        { value: "title", name: "По названию" },
        { value: "body", name: "По содержимому" },
      ],
    };
  },

  methods: {
    CreatePost(post) {
      this.posts.push(post);
      this.dialodVisible = false;
    },
    RemovePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showDialog() {
      this.dialodVisible = true;
    },
    async fetchPost() {
      //реализуем ассинхронную функцию. для того чтобы отлавливать ошибки обернем код в блок try catch
      try {
        this.isPostLoading = true;

        const response = await axios.get(
          //библиотека ахсиус для запросов тут реализум запрос на сервер и помещаем ответ в переменную
          "https://jsonplaceholder.typicode.com/posts",
          { params: { _page: this.limit, _limit: this.limit } }
        );
        this.TotalPages = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        this.posts = response.data;
      } catch (e) {
        alert("Ошибка");
      } finally {
        this.isPostLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPost(); //подгрузка постов динамически в хуке
  },
  computed: {
    sottedPosts() {
      return [...this.posts].sort((post1, post2) =>
        post1[this.selectedSord]?.localeCompare(post2[this.selectedSord])
      );
    },
    sorteAndSearchedPost() {
      return this.sottedPosts.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },

  watch: {
    sorteAndSearchedPost(newValue) {
      console.log(newValue);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.title {
  margin: 10px;
}
.app__btns {
  display: flex;
  justify-content: space-between;
}
.page__wrapper {
  display: flex;
  margin-top: 15px;
}
.page {
  border: 1px solid black;
  padding: 10px;
}
.current-page {
  border: 2px solid black;
}
</style>

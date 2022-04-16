<template>
  <div class="app">
    <PostForm @create="CreatePost" />
    <PostList :posts="posts" @remove="RemovePost"/>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
export default {
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [
        //массив постов
        {
          id: 1, //тело
          title: "java",
          body: "Описание поста",
        },
        {
          id: 2,
          title: "java 2",
          body: "Описание поста 2",
        },
        {
          id: 3,
          title: "java 3",
          body: "Описание поста 3",
        },
        {
          id: 4,
          title: "java 4",
          body: "Описание поста 4",
        },
      ],
    };
  },

  methods: {
    CreatePost(post) {
      this.posts.push(post);
    },
    RemovePost(post){
      this.posts= this.posts.filter(p=>p.id !== post.id)
    }
  }, 
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

</style>

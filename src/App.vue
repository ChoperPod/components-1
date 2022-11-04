<script setup>
import { ref } from 'vue';
import BlogPost from './Components/BlogPost.vue';
import ButtonCounter from './Components/ButtonCounter.vue'
import PaginatePost from './Components/PaginatePost.vue'

const posts = ref([
/*  { title: 'post 1', id: 1, body: 'descripcion 1', colorText: "primary" },
  { title: 'post 2', id: 2, body: 'descripcion 2', colorText: "secondary" },
  { title: 'post 3', id: 3, body: 'descripcion 3', colorText: "success" },
  { title: 'post 4', id: 4, colorText: "danger" },*/

])

const favorito = ref('');
const CambiarFavorito = (title) => {
  favorito.value = title
};

fetch('https://jsonplaceholder.typicode.com/posts')
.then((res) => res.json())
.then((data) => {posts.value = data;});//console.log(data))


</script>


<template>
  <div class="container">
    <h1>APP</h1>
    <h2>Mi post favorito: {{favorito}}</h2>
    <PaginatePost class="mb-2"/><br>
    <!--<button @click="increment">{{ counter }}</button>-->
    <ButtonCounter />
    <button-counter />
    <br><br>
    <BlogPost 
      v-for="post in posts.slice(0,10)" 
      :key="post.id" 
      :title="post.title" 
      :id="post.id" 
      :body="post.body"
      :CambiarFavorito="CambiarFavorito"
      class="mb-2">
    </BlogPost><br>

  </div>
</template>

<style>

</style>
<script setup>
import { onMounted, ref } from 'vue';
import BlogPost from './Components/BlogPost.vue';
import ButtonCounter from './Components/ButtonCounter.vue'
import PaginatePost from './Components/PaginatePost.vue'
import LoadingSp from "./Components/LoadingSp.vue"

const posts = ref([])
const PostxPag = 10
const inicio = ref(0)
const fin = ref(PostxPag)
const loading = ref(true)
const next = () => {
  inicio.value = inicio.value + PostxPag
  fin.value = fin.value + PostxPag
}
const prev = () => {
  inicio.value = inicio.value - PostxPag
  fin.value = fin.value - PostxPag
}

const favorito = ref('');
const CambiarFavorito = (title) => {
  favorito.value = title
};

// Opcion correcta para consumir API´s
const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally {
    setTimeout(() => {
      loading.value = false
    }, 1300);
  }
};

fetchData();
// onMounted(async () => {
//   //loading.value = true
//   try {
//     const res = await fetch('https://jsonplaceholder.typicode.com/posts')
//     posts.value = await res.json()
//   } catch (error) {
//     console.log(error)
//   } finally {
//     setTimeout(() => {
//       loading.value = false
//     }, 1300);
//   }
// });

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then((res) => res.json())
//   .then((data) => { posts.value = data; })
//   .finally(() => {
//     setTimeout(() => {
//       loading.value = false
//     }, 1300);
//   })
</script>


<template>
  <LoadingSp v-if="loading" />
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{ favorito }}</h2>
    <PaginatePost @next="next" @prev="prev" class="mb-2" :inicio="inicio" :fin="fin" :maxLength="posts.length" /><br>
    <!--<button @click="increment">{{ counter }}</button>-->
    <ButtonCounter />
    <button-counter />
    <br><br>
    <BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.id" :title="post.title" :id="post.id"
      :body="post.body" :CambiarFavorito="CambiarFavorito" class="mb-2">
    </BlogPost><br>
  </div>
</template>

<style>

</style>
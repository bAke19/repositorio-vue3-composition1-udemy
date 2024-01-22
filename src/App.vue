<script setup>

import {ref, onMounted} from "vue";
import BlogPost from './components/BlogPost.vue';
import PaginacionPost from './components/PaginacionPost.vue';
import LoadingSpinner from "./components/LoadingSpinner.vue"

const posts = ref([])

const miFavorito = ref("");
const loading = ref(true);

const cambiarFavorito = (title) => {
    miFavorito.value = title;
};

const fetchData = async() => {
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()
  } catch (error){
    console.log(error)
  } finally {
    loading.value = false
  }
}
onMounted(async() => {
  fetchData();
})

//recomendable
/* fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res=>res.json())
  .then(response => {
    posts.value = response
    
  })
  .catch(error => console.log(error))
  .finally(() => {
    setTimeout(() => {
      loading.value = false
    }, 2000)
    
  }) */

const postXPagina = 5
const indexPostPrincipioPagina = ref(0)
const indexPostFinalPagina = ref(postXPagina)


const nextPage = () =>{
  indexPostPrincipioPagina.value += postXPagina
  indexPostFinalPagina.value += postXPagina
}

const previewPage = () =>{
  indexPostPrincipioPagina.value -= postXPagina
  indexPostFinalPagina.value -= postXPagina
}


</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1>App1</h1>
    <h2>
      Mi post favorito: {{ miFavorito  }}
    </h2>
    <PaginacionPost 
      class="mb-2"
      @nextPage = "nextPage"
      @previewPage = "previewPage"
      :inicio = "indexPostPrincipioPagina"
      :final = "indexPostFinalPagina"
      :max = "posts.length"
      />
    <BlogPost
      v-for="post in posts.slice(indexPostPrincipioPagina,indexPostFinalPagina)"  
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :text="post.body"
      @cambiarFavoritoNombre="cambiarFavorito"
      class="mb-2"
    ></BlogPost>
  </div>
  
</template>

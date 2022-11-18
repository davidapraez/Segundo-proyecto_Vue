<script setup>
import { ref } from 'vue';
import ButtonCounter from './components/ButtonCounter.vue'
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';


/*const posts= ref([
  {title:'Post 1', id:1,body:'descripcion 1'},
  {title:'Post 2', id:2,body:'descripcion 2'},
  {title:'Post 3', id:3,body:'descripcion 3'},
  {title:'Post 4', id:4},
])*/
//V
const posts=ref([])
const xpag=10
const inicio=ref(0)
const fin=ref(xpag)
  
const favorito=ref("")
const cambiarFavorito=(title)=>{
  favorito.value=title;
}

const next=()=>{
  inicio.value=inicio.value+xpag;
  fin.value=fin.value+xpag;
}

const prev=()=>{
  inicio.value+= -xpag;
  fin.value+= -xpag;
}
// Es mejor Usar el Emit para las funciones y no pasar las funciones como props

fetch('https://jsonplaceholder.typicode.com/posts')
.then(res=>res.json())
.then((data)=>posts.value=data)

console.log("Agregando cambios");
</script>

<template>
  <div class="container">
    <h1 >App</h1>
    <ButtonCounter></ButtonCounter>
    
    <!-- Esta es la primera forma de realizar los objetos-->
    <!--
    <BlogPost title="Post1" :id="1" body="descripcion 1" colorText="primary"></BlogPost>
    <BlogPost title="Post2" :id="2" body="descripcion 2" colorText="secondary"></BlogPost>
    <BlogPost title="Post3" :id="3" body="descripcion 3" colorText="success"></BlogPost>
    <BlogPost title="Post4" :id="4" body="descripcion 4" colorText="primary"></BlogPost>
    -->
    <!--Segunda forma de crear los objetos recorriendo el objeto-->
    <h2 >Mi post favoritos: {{favorito}}</h2>
    <button @click="next">Next provisorio</button>
    <button @click="prev">Prev provisorio</button>
    <PaginatePost class="mb-2 positive"/>  
    <BlogPost
    v-for="post in posts.slice(inicio,fin)"
    :key="post.id"
    :title="post.title"
    :id="post.id"
    :body="post.body"
    :cambiarFavorito="cambiarFavorito"
    class="mb-2"

    ></BlogPost>



    
  </div>
</template>

<style>
.container{
  background-color: beige;
  color: black;
}
.positive{
  color:aqua
}
.negative{
  color:red
}
.zero{
  color: tomato
}
</style>
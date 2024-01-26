<script setup>
import ButtonCounter from './components/ButtonCounter.vue';
import Blogpost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
import { ref, computed , onMounted } from "vue";



/*const posts = ref([
  {title: 'Post 1', id: 1, body: 'descripcion 1'},
  {title: 'Post 2', id: 2, body: 'descripcion 2'},
  {title: 'Post 3', id: 3, body: 'descripcion 3'},
  {title: 'Post 4', id: 4},
])
*/

const posts = ref([]);

const postxpage = 1
const inicio = ref(0)
const final = ref(postxpage)
const loading = ref(true);

const favorito = ref("")

const cambiarFavorito = (title) => {
  favorito.value = title;
}

const next = () => {
  inicio.value += postxpage;
  final.value += postxpage;
};

const previus = () => {
  inicio.value -= postxpage;
  final.value -= postxpage;
};
/*
onMounted(async() => {
 loading.value = true;
 try{
  const res = await fetch('https://jsonplaceholder.typicode.com/posts')
  posts.value = await res.json()
 } catch(error) {
  console.log(error)
 } finally {
  setTimeout(() => {
      loading.value = false;
    },4000);
 }
   fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data => {
    posts.value = data;
  })
  .finally(() => {
    setTimeout(() => {
      loading.value = false;
    },4000);
    
  })
})*/
  const maxLenght = computed (() => posts.value.length);

  const fetchData = async ()  => {
    try{
        const res = await fetch('https://jsonplaceholder.typicode.com/posts')
        posts.value = await res.json()
    } catch(error) {
         console.log(error);
    } finally {
        setTimeout(() => {
            loading.value = false;
        },4000);
    }
  };
  fetchData();
</script>

<template>

  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito {{ favorito }}</h2>
    <ButtonCounter />
  
    <button-counter></button-counter><br><br>

    

    <PaginatePost class="mb-2" 
    @next="next" 
    @previus="previus" 
    :inicio="inicio" 
    :final="final"
    :maxLength = "posts.length"
    >
      
    </PaginatePost>
    

   

    <Blogpost 
    v-for="post in posts.slice(inicio,final)"
    :key="post.id"
    :title="post.title"
    :id="post.id"
    :body="post.body"
    @cambiarFavoritoNombre="cambiarFavorito"
    class="mb-2"
    >
    
    </Blogpost>
    <!-- 
      <Blogpost title="Post 02" :id="2" body="descripcion 2" colorText="secundary"/>
    <Blogpost title="Post 03" :id="3" body="descripcion 3" colorText="success"/>
    <Blogpost title="Post 04" :id="4" colorText="primary"/>
    -->
  </div>
  
  
</template>

<!--
   <script>
export default{
  data(){
    return {
      counter: 0
    }
  },
  methods: {
    increment(){
      this.counter ++
    }
  }
}

</script>
  
  
  <script>
import { ref } from 'vue'

export default {
  setup(){

    const counter = ref(0);

    const increment = () => {
      counter.value ++
    }
    return{
      counter,
      increment,
    };
  }
}

</script>

<template>
  <h1>APP</h1>
  <button @click="increment">{{counter}}</button>
</template>
 -->


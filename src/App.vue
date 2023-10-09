<script setup>
import BlogPost from './components/BlogPost.vue';
import {ref, onMounted} from 'vue';
import PaginatePost from './components/PaginatePost.vue';
import SpinnerLog from './components/SpinnerLog.vue';

const posts = ref([]);
const postXpage = 4;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const fav = ref("");

const cambiarFav = (title) => {
    fav.value = title;
};

const next = () =>{
    inicio.value = inicio.value + postXpage
    fin.value = fin.value + postXpage
};

const prev = () =>{
    inicio.value = inicio.value - postXpage
    fin.value = fin.value - postXpage
}

// onMounted(async()=>{
//     try {
//        const res = await fetch('https://jsonplaceholder.typicode.com/posts');
//        posts.value = await res.json();
//     } catch (error) {
//         console.log(error)   
//     }  finally {
//         setTimeout(()=>{
//             loading.value = false;
//         }, 1200)
//     }
// })

// fetch ('https://jsonplaceholder.typicode.com/posts')
//     .then((res) => res.json())
//     .then((data) => {
//     posts.value = data
//     })
//     .finally(() => {
//         setTimeout(()=>{
//         loading.value = false
//         },1200)
//     });

const fetchData = async() => {
    try {
       const res = await fetch('https://jsonplaceholder.typicode.com/posts');
       posts.value = await res.json();
    } catch (error) {
        console.log(error)   
    }  finally {
        setTimeout(()=>{
            loading.value = false;
        }, 1200)
    }
};

fetchData();

</script>

<template>
    <SpinnerLog v-if="loading"/>
    <div class="container" v-else>
        <h1>Web Components</h1>
        <h2>Mi Post Favorito: {{ fav }}</h2>
        <PaginatePost 
            @next='next' 
            @prev='prev' 
            :inicio='inicio' 
            :fin='fin'
            :maxLength='posts.length'
        />
        <blog-post 
            v-for="post in posts.slice(inicio, fin)"
            :key='post.id'
            :title="post.title" 
            :id='post.id' 
            :body='post.body'
            @cambiarFavName="cambiarFav" 
        ></blog-post>
    </div>
</template>



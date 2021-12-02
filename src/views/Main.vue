<template>
<div>
    <carrito-1></carrito-1>
    
<!-- <h2>Parámetro: {{ $route.params.id }}</h2> -->
<div class="container " >
    <div class="row align-items-start">
    Estrenos
    </div>
    <keep-alive>
  <div class="d-flex flex-row bd-highlight mb-3">
      <div v-for="item in arrayBlog" :key="item.filmId">
    
      
      <div class="card " style="width: 18rem;">
  <img src="https://picsum.photos/200/300?random=2" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">{{ item.title }}</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <router-link :to="`/film/${item.filmId}`">
        {{ item.title }}
      </router-link>
  
  </div>
        
      
  </div>
    </div>
    
  </div>
  </keep-alive>
  <div class="row align-items-start">
    Estrenos
    </div>
  <div class="d-flex flex-row bd-highlight mb-3">
      <div v-for="item in arrayTop" :key="item.filmId">
    
      
      <div class="card " style="width: 18rem;">
  <img src="https://picsum.photos/200/300?random=2" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">{{ item.title }}</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <router-link :to="`/film/${item.filmId}`">
        {{ item.title }}
      </router-link>
  
  </div>
        
      
  </div>
    </div>
    
  </div>
  <div class="row">
    
  </div>
</div>

</div>
</template>

<script>
import Carrito1 from '../components/Carrito1.vue'
export default {
    components: {
        Carrito1
    },
    data() {
        return {
            arrayBlog: [],
            arrayTop: []
        }
    },
    methods: {
        async consumirApi(){
            try {
                const data = await fetch(`http://localhost:8080/main/${this.$route.params.id}`)
                const array = await data.json()
                console.log(array)
                this.arrayBlog = array;
               
            } catch (error) {
                console.log(error)
            }
            
        },
        async consumirApi2(){
            try {
                const data1 = await fetch(`http://localhost:8080/main1/${this.$route.params.id}`)
                const array1 = await data1.json()
                console.log("top10")
                console.log(array1)
                this.arrayTop = array1;
                
            } catch (error) {
                console.log(error)
            }
            return
        }

    },
    
    
    created() {
        this.consumirApi();
        this.consumirApi2();
    
    }
}
</script>

<style>

</style>
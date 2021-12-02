<template>
<div>
    <carrito-1></carrito-1>
<a href="javascript:history.back()"> <button  class="btn btn-outline-success" type="submit">Volver atras</button></a>
<div class="container " >
    <div class="row align-items-start">
    Estrenos
    </div>
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
            arrayTop: [],
            name: String,
            surname: String,
            temp: String
        }
    },
    methods: {
        async consumirApi(){
            try {
                this.seParar()
                const data = await fetch(`http://localhost:8080/actor/${this.name}/${this.surname}`)
                const array = await data.json()
                console.log(array)
                this.arrayBlog = array;
               
            } catch (error) {
                console.log(error)
            }
            
        },
        seParar(){
            this.temp=this.$route.params.title
            var nameArray=this.temp.split(" ")
            this.name=nameArray[0]
            this.surname=nameArray[1]


        }
       

    },
    
    
    created() {
        this.consumirApi();
        
    
    }
}
</script>

<style>

</style>
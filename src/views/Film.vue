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
    <button type="button" class="btn btn-outline-info" @click="AgregarCarrito(item.filmId,item.title)">Agregar Al Carrito</button>
  
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
            filmlist: []
        }
    },
    methods: {
        async consumirApi(){
            try {
                const data = await fetch(`http://localhost:8080/film/${this.$route.params.title}`)
                const array = await data.json()
                console.log(array)
                this.arrayBlog = array;
               
            } catch (error) {
                console.log(error)
            }
            
        },
       
      AgregarCarrito(id,title){
            
      this.filmlist.push({Id: id, Title: title});
      this.saveCarrito();

        },
        saveCarrito(){
            const parsed = JSON.stringify(this.filmlist);
      localStorage.setItem('films', parsed);
      var guardado = localStorage.getItem('films');
      console.log('objetoObtenido: ', JSON.parse(guardado))
        }

    },
    
    mounted() {
        if (localStorage.getItem('films')) {
      try {
        this.filmlist = JSON.parse(localStorage.getItem('films'));
      } catch(e) {
        localStorage.removeItem('films');
      }
    }
    },
    created() {
        this.consumirApi();
        
    
    }
}
</script>

<style>

</style>
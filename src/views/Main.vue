<template>
<div>
    <carrito-1></carrito-1>
    <br>
<!-- <h2>Parámetro: {{ $route.params.id }}</h2> -->
<div class="alert alert-success" role="alert">
  <h4 class="alert-heading">Bienvenid@</h4>
  <p>Nos alegra tenerte aqui</p>
  <p>🎉🎉¿Aun no te registras? Sigue el siguiente boton para registrarte! 🎉🎉</p>
  <hr>
  <router-link :to="`/datos/${$route.params.id}`">
        <button type="button" class="btn btn-outline-success">Registrarse</button></router-link>
</div>

<div class="container " >
    <div class="row align-items-start">
    🎥Las Mas Vistas Todos los tiempos🎥
    </div>
    <keep-alive>
  <div class="d-flex flex-row flex-nowrap overflow-auto">
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
  </keep-alive>
  <div class="row align-items-start">
   🎥 Estrenos🎥
    </div>
  <div class="d-flex flex-row flex-nowrap overflow-auto">
      <div v-for="item in arrayTop" :key="item.filmId">
    
      
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
  <div class="row align-items-start">
    🎥Las Mas vistas la ultima semana🎥
    </div>
  <div class="d-flex flex-row flex-nowrap overflow-auto">
      <div v-for="item in arrayWeek" :key="item.filmId">
    
      
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
            arrayWeek: [],
            filmlist: []
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
        },
        async consumirApi3(){
            try {
                const data1 = await fetch(`http://localhost:8080/main2/${this.$route.params.id}`)
                const array1 = await data1.json()
                console.log("top10")
                console.log(array1)
                this.arrayWeek = array1;
                
            } catch (error) {
                console.log(error)
            }
            return
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
        this.consumirApi2();
        this.consumirApi3();
    
    }
}
</script>

<style>

</style>
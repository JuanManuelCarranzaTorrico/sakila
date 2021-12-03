<template>
<div>
  
  <nav class="navbar navbar-light" style="background-color: #e3f2fd;">
    
    <div class="container-fluid ">
   
    <form class="d-flex">
      <h2>Sakila</h2>
      <input class="form-control me-2" type="text" v-model="texto" placeholder="Search" aria-label="Search">
      <router-link :to="`/film/${texto}`">
        <button  class="btn btn-outline-success" type="submit">Titulo</button>
        </router-link>
      <router-link :to="`/actor/${texto}`">
        <button  class="btn btn-outline-success" type="submit">Actor</button>
        </router-link>
        
    </form>
    <router-link :to="`/carrito/${this.$route.params.id}`">
       <button type="button" class="btn btn-outline-warning">Carrito</button>
       </router-link>
  </div>
 
  
</nav>

</div>
</template>

<script>

export default {
  components:{

  },
 props:{
     id: String,
     texto: String
 },
 methods: {
    // buscarActor(){
    //     console.log("Se busco actor")
    //     alert("se busca "+this.texto)
    // },
    // buscarFilm(){
    //     console.log("Se busco film")
    // }
}
}

</script>

<style>

</style>
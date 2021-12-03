<template>
<div>
<carrito-1></carrito-1>
<br>
<div class="d-grid gap-2">
    <router-link :to="`/main/${this.$route.params.id}`">
  <button type="button" class="btn btn-outline-success">Volver atras</button>
    </router-link>
</div>
  <div class="container">
     <div class="row">
      <div class="col-5">
          <div v-for="item in filmlist" :key="item.Id">
            <div class="card mb-3" style="max-width: 540px;">
  <div class="row g-0">
    <div class="col-md-4">
      <img src="https://picsum.photos/200/300?random=2" class="img-fluid rounded-start" alt="...">
    </div>
    <div class="col-md-8">
      <div class="card-body">
        <h5 class="card-title">{{item.Title}}</h5>
        <p class="card-text">Precio: <br> 0.99$</p>
        <p class="card-text">
            <button type="button" class="btn btn-outline-danger" @click="removeCarrito(item)">Eliminar del Carrito</button>
  
        </p>
      </div>
    </div>
  </div>
</div>
    </div>
          </div>
          
          <div class="col-5">

              <h2>Dias</h2>
              <input min=1 max=7 type="number" v-model="days">
              <h2>Cantidad</h2>
              {{CalcularTotal}} Bs
              <h2>Descuento</h2>
              {{des * 100}} %
              <h2>Cantidad Total</h2>
              {{total}} Bs
              <h2>Comfirmar Pedido</h2>
              <form>
  <div class="form-group">
    <label for="exampleInputEmail1">Ingresa tu id de cliente</label>
    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
  </div>
  <h3>Total:</h3>
  <br>
  <div>

          </div>
  <button type="button" class="btn btn-outline-info"  @click="consumirPost()">Confirmar Pedidos</button>
  
</form>
              
          </div>
      
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
            filmlist: [],
            film: [],
            total: 0.0,
            store:0,
            days: 1,
            des: 0,

        }
    },
    methods: {
        
        verCarrito(){
            var guardado = localStorage.getItem('films');
            this.filmlist=guardado
            console.log('objetoObtenido: ', JSON.parse(guardado))
            this.store=this.$route.params.id
            // this.CalcularTotal(guardado)
        },
        removeCarrito(film){
            this.filmlist.splice(film,1);
            this.saveCarrito()

        },
        saveCarrito(){
            const parsed = JSON.stringify(this.filmlist);
      localStorage.setItem('films', parsed);
      var guardado = localStorage.getItem('films');
      console.log('objetoObtenido: ', JSON.parse(guardado))
        },
        EliminarCarrito(){
            storage.clear();
        },
        
        async consumirPost(){

          var len=(this.filmlist.length);
          console.log(len)
          var i=0
          for(i=0;i<len;i++){
              var idf=this.filmlist[i]['Id']
              console.log(idf)
              this.PostPetition(idf)
              this.removeCarrito(this.filmlist[i])
          }

        },

        async PostPetition(f){
          try {
                const data = await fetch(`http://localhost:8080/rental`,{
                    method: `POST`,
                    body: JSON.stringify({
                        rentalId : 1,
                        inventoryId: parseInt(f),
                        customerId : 1,
                        staffId: parseInt(this.$route.params.id),
                    }),
                    headers: {
                        "Content-Type": "application/json" 
                        },
                })
                console.log("Registro exitoso :3")

                console.log(await data)
               
            } catch (error) {
                console.log(error)
                console.log("algo salio mal")
            }
        }
        
}, computed: {
CalcularTotal(){

            //10 15 20
            
            let FilmNumber = this.filmlist.length;
            let dineros = FilmNumber * 0.99 * this.days
            if (dineros < 10){
              this.des = 0
            } 
            if (dineros >= 10 && dineros < 15){
              this.des = 0.10
            } 
            if (dineros >= 15 && dineros < 20){
              this.des = 0.15
            } 
            if (dineros >= 20){
              this.des = 0.20
            } 
            this.total = dineros * (1-this.des)
            return dineros;
        },
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
    this.verCarrito()
    
},

}
</script>

<style>

</style>
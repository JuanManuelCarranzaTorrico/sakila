<template>
  <div>
<div class="modal-body row">
  <div class="col-md-6">
   <div class="mb-3">
       <h1>Crear Usario</h1>
       <div class="input-group">
  <span class="input-group-text">Nombre y Apellido</span>
  <input type="text" aria-label="First name" v-model="nombre" class="form-control">
  <input type="text" aria-label="Last name" v-model="Apellidos" class="form-control">
</div>
</div>
<div class="row g-2">
  <div class="col-md">
    <div class="form-floating">
      <input type="email" class="form-control" v-model="Email" id="floatingInputGrid"  >
      <label for="floatingInputGrid">Direccion de correo electronico</label>
    </div>
  </div>
  <div class="col-md">
    <div class="form-floating">
      <div class="form-floating">
      <input type="number" class="form-control" v-model="addressId" id="floatingInputGrid"  >
      <label for="floatingInputGrid">Numero de direccion</label>
    </div>
    </div>
  </div>
</div>
<br>
<button type="submit" class="btn btn-secondary" @click="prueba1()" >Crear</button>
  </div>
  <div class="col-md-6">
   <h1>Crear Usario</h1>
       <div class="input-group">
  <span class="input-group-text">Nombre y Apellido</span>
  <input type="text" aria-label="First name" v-model="nombre" class="form-control">
  <input type="text" aria-label="Last name" v-model="Apellidos" class="form-control">
</div>
<select class="form-select form-select-lg mb-3"  v-model="selected" aria-label="Default select example">
    
  <option value="189">Graz</option>
  <option value="307">Linz</option>
  <option value="447">Salzburg</option>
  <option value="565">Vancouver</option>
  <option value="383">Oshawa</option>
  <option value="430">Rinchmond Hill</option>
  <option value="300">Lethbridge</option>


</select>
<button type="button" class="btn btn-secondary" @click="prueba2()" >Crear</button>
  </div>
</div>

  </div>
</template>

<script>
export default {
    data() {
        return {
        
        }
    },
    prop: {
        nombre: String,
        Apellidos: String,
        Email: String,
        storeId: 0,
        addressId :0,
        selected: ""
        
    },
    methods: {
        prueba1(){
            console.log("nombre: "+this.nombre);
            console.log("Apellido: "+this.Apellidos);
            console.log("email: "+this.Email);
            console.log(this.addressId);
            this.storeId=this.$route.params.id
            console.log("tienda "+this.storeId)
            this.consumirPost()


        },
        prueba2(){
            alert(this.selected)

        },
        async consumirPost(){
            try {
                const data = await fetch(`http://localhost:8080/customer`,{
                    method: `POST`,
                    body: JSON.stringify({
                        customerId : 1,
                        storeId: parseInt(this.storeId),
                        firstName : this.nombre,
                        lastName: this.Apellidos,
                        email : this.Email,
                        addressId : parseInt(this.addressId),
                        active: 1
                    }),
                    headers: {
                        "Content-Type": "application/json" 
                        },
                })
                alert("Registro exitoso :3")
                // .then(response => response.json())
                // .then((json)=> console.log(json));

                // const array = await data.json()
                // console.log(array)
                // this.arrayBlog = array;
                console.log(await data)
               
            } catch (error) {
                console.log(error)
                console.log("algo salio mal")
            }
            
        }
    },
     

}
</script>


<style>

</style>
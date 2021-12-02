<template>
  <div>
<div class="modal-body row">
    <router-link :to="`/main/${this.$route.params.id}`">
    <button type="button" class="btn btn-outline-success">Volver al inicio</button>
        </router-link>
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
  <span class="input-group-text">Direccion y distrito</span>
  <input type="text" aria-label="First name" v-model="addres" class="form-control">
  <input type="text" aria-label="Last name" v-model="district" class="form-control">
</div>
<label for="exampleFormControlInput1" class="form-label">Seleccione su ciudad</label>
<select class="form-select form-select-lg mb-3"  v-model="selected" aria-label="Default select example">
    
  <option value="189">Graz</option>
  <option value="307">Linz</option>
  <option value="447">Salzburg</option>
  <option value="565">Vancouver</option>
  <option value="383">Oshawa</option>
  <option value="430">Rinchmond Hill</option>
  <option value="300">Lethbridge</option>
  <option value="179">Gatineau</option>
</select>

 <div class="input-group">
  <span class="input-group-text">Codigo Postal y telefono</span>
  <input type="text" aria-label="First name" v-model="postalCode" class="form-control">
  <input type="text" aria-label="Last name" v-model="phone" class="form-control">
</div>

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
        selected: "",
        addres: "",
        district: "",
        postalCode: "",
        phone: ""

        
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
            console.log(this.addres)
            console.log(this.district)
            console.log(this.selected)
            console.log(this.postalCode)
            console.log(this.phone)
            this.consumirPost1()

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
            
        },
        async consumirPost1(){
            try {
                const data = await fetch(`http://localhost:8080/address`,{
                    method: `POST`,
                    body: JSON.stringify({
                        addresId : 1,
                        address: this.addres,
                        address2: "",
                        district: this.district,
                        city : parseInt(this.selected),
                        postalCode : this.postalCode,
                        phone: this.phone
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
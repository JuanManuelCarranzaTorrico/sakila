<template>
<div>
<div class="home">
    <div class="alert alert-info" role="alert">
  <h1>Sakila video club </h1>
</div>
</div>
<div class="container">

    <div class="row">
      <div class="col-lg-6"  style="background-color:#aaa">
        <h1>Canada</h1> 
        <router-link :to="`/main/2`">
        <button type="button"> <img src="https://imagenesnoticias.com/wp-content/uploads/2019/01/1-2.jpg" height ="80" width="100" /></button>
        </router-link>
      </div>
      <div class="col-lg-6"  style="background-color:#bbb">
        <h1>Australia</h1> 
        
        
        
        
        <router-link :to="`/main/1`">
        <button type="button"> <img src="https://www.ecured.cu/images/d/d6/125px-Flag_of_Australia.svg.png" height ="80" width="100" /></button>
        </router-link>

      </div>
    </div>

  </div> 
</div>
</template>

<script>
const au=1
const ca=2
</script>

<style>

</style>
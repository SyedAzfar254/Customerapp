<template>

  <div id="app">  
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#"> vCustomers </a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarText">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
       <router-link to="/about"> About </router-link>
       <router-link to="/"> Home </router-link>
      </li>
    </ul>
    <span>
    <li class="nav-item active">
    <router-link to="/add">  </router-link>
    </li>
    </span>
  </div>
</nav>


     <router-view></router-view>
     </div>

</template>

<script>

export default {
 name : 'app',
 components : {
 }
}

</script>

<style>

</style>

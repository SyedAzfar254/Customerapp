<template>
  <div class="details container">
    <router-link to="/">Back</router-link>     
  <h1 class = "page-header"> {{customer.first_name}} {{customer.last_name}}</h1>
    
    
   <ul class="list-group">
      <li class="list-group-item"> <span class="glyphicon glyphicon-phone" aria-hidden = "true"> </span> {{customer.phone}} </li>
      <li class="list-group-item"> <span class="glyphicon glyphicon-envelope" aria-hidden = "true"> </span> {{customer.email}} </li>
    </ul>

    <ul class="list-group"> 
        <li class="list-group-item">{{customer.address}}</li>
        <li class="list-group-item">{{customer.city}}</li>
        <li class="list-group-item">{{customer.state}}</li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data (){
    return {
     customer:''
    }
  },
  methods:{
    fetchCustomer(id){
       this.$http.get('http://localhost:8888/v2/public/api/customer/' +id)
      .then(function (response){
       this.customer = response.data;
      });
  },
  

}, 

created: function (){
  this.fetchCustomer(this.$route.params.id);
}

}
</script>



<style scoped>

</style>
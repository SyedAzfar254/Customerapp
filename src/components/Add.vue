<template>
  <div class="add container">
    <Alert v-if="alert" v-bind:message="alert"/>
    <h1 class = "page-header"> Add Customer </h1>
  <form v-on:submit="addCustomer">
   <div class="form-group">
   <h4> Customer Name </h4>
    <label for="exampleInputEmail1">First Name</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter First Name" v-model="customer.first_name">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">Last Name</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter Last Name" v-model="customer.last_name">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>

   <div class="form-group">
   <h4> Customer Contact </h4>
    <label for="exampleInputEmail1">Email</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter Email" v-model="customer.email">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">Phone number</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter Phone Number" v-model="customer.phone">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>

  <div class="form-group">
  <h4> Customer Location </h4>
    <label for="exampleInputEmail1">Address</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter Address" v-model="customer.address">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">City</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter City" v-model="customer.city">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">State</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter State" v-model="customer.state">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>

  </form>
  </div>
</template>

<script>
import Alert from './Alert'

export default {
  name: 'add',
  data (){
    return {
     customer: {},
     alert:''
    }
  },
  methods:{
    
  },
  components: {
    Alert
  }
}
</script>



<style scoped>


</style>

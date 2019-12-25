<template>
  <div class="customers container">
    <h3>
  <strong>Manage Customers App </strong>
</h3>
    <Alert v-if="alert" v-bind:message = "alert"/> 
       <button type="button" class="btn btn-primary" data-toggle="modal" @click="OpenAddModal" style="margin-top:20px; margin-bottom:20px">Add</button>
   <input class="form-control" placeholder="Enter Last Name" v-model="filterInput">
   <br/>  
   <table class="table">
  <thead>
    <tr>
      <th> First name </th>
      <th> Last name </th>
      <th> Email </th>
      <th> </th>
    </tr>
  </thead>
  <tbody>
    
    <tr v-for = "customer in filterBy(customers,filterInput)" :key="customer.id "> 
     <td> {{customer.first_name}}</td>
     <td> {{customer.last_name}}</td>
     <td> {{customer.email}}</td>
     <td> <router-link class="btn btn-outline-dark " v-bind:to="'/customer/'+customer.id">View</router-link></td>
   <button type="button" class="btn btn-outline-primary" data-toggle="modal" @click="OpenEditModal(customer.id)" style="margin-top: 15px;">Edit</button>
   <button type="button" class="btn btn-outline-danger" @click="deleteCustomer(customer.id)" style=" margin-top: 15px; margin-left: 10px;">Delete</button> 
    </tr>
  </tbody>
</table>
  <!-- Button trigger modal -->


<!-- Modal -->
<div class="modal fade" id="addModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Edit Customer</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">  
                               <!-- Edit Form -->
       <form v-on:submit="validateForm" >

   <div class="form-group">
   <h4> Customer Name </h4>
    <label for="exampleInputEmail1">First Name</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter First Name" v-model="customer.first_name">
    <small id="emailHelp" class="form-text text-muted"></small>
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">Last Name</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter Last Name" v-model="customer.last_name">
    <small id="emailHelp" class="form-text text-muted"></small>
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
    <small id="emailHelp" class="form-text text-muted"></small>
  </div>

  <div class="form-group">
  <h4> Customer Location </h4>
    <label for="exampleInputEmail1">Address</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter Address" v-model="customer.address">
    <small id="emailHelp" class="form-text text-muted"></small>
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">City</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter City" v-model="customer.city">
    <small id="emailHelp" class="form-text text-muted"></small>
  </div>
  <div class="form-group">
    <label for="exampleInputEmail1">State</label>
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter State" v-model="customer.state">
    <small id="emailHelp" class="form-text text-muted"></small>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>

  </form>                      
  
      </div>
      <div class="modal-footer">
      </div>
    </div>
  </div>
</div>

  </div>

</template>

<script>
import Alert from './Alert' ;
import swal from 'sweetalert'
export default {
  name: 'customers',
  data (){
    return {
      editmode: false,
      customers: [],
      customer: {},      
      alert:'', 
      filterInput:''

    }
  },

  methods: {
     OpenEditModal(id)
     {
      Bus.$emit('afterCreated');
      this.editmode = true
      $('#addModal').modal('show')
      this.fetchCustomer(id);
      
  
     },
     OpenAddModal()
     {
       this.customer = [];
       Bus.$emit('afterCreated');
      this.editmode = false
      $('#addModal').modal('show')
      
     },
             
             // Edit methods //

     fetchCustomer(id){
       this.$http.get('http://localhost:8888/v2/public/api/customer/' +id)
      .then(function (response){
       this.customer = response.data;
       });
       },
               //Delete method //
        
        deleteCustomer(id){
   this.$http.delete('http://localhost:8888/v2/public/api/customer/delete/' +id)
      .then(function (response){
       swal("Customer Deleted");
       Bus.$emit('afterCreated');
      });
},
 
             //Edit Methods Continues//

       updateCustomer(e){
      if (! this.customer.first_name || ! this.customer.last_name || ! this.customer.email){
        this.alert= 'Fill in all required feilds';   
      }
      else {
        let updCustomer = {
          first_name : this.customer.first_name,
          last_name : this.customer.last_name,
          phone : this.customer.phone,
          email : this.customer.email,
          address: this.customer.address,
          city : this.customer.city,
          state : this.customer.state
        }
         
         this.$http.put('http://localhost:8888/v2/public/api/customer/update/' +this.customer.id, updCustomer )
         
         .then(function(){
           swal("Customer Updated"); 
          $('#addModal').modal('hide')
           Bus.$emit('afterCreated');
         }) 

        e.preventDefault(); 
      }
     e.preventDefault();
    },

    validateForm(e){
       if (this.editmode == true){
         this.updateCustomer(e);
       }
       else {
         this.addCustomer(e);
       }
    },

        // Add Methods //

       addCustomer(e){
      if (! this.customer.first_name || ! this.customer.last_name || ! this.customer.email){
        this.alert = 'Fill in all required feilds ';   
      }
      else {
        let newCustomer = {
          first_name : this.customer.first_name,
          last_name : this.customer.last_name,
          phone : this.customer.phone,
          email : this.customer.email,
          address: this.customer.address,
          city : this.customer.city,
          state : this.customer.state
        }
         
         this.$http.post('http://localhost:8888/v2/public/api/customer/add', newCustomer )
         .then(function(){
           swal("Customer Added"); 
          $('#addModal').modal('hide')
          Bus.$emit('afterCreated');
          
         }) 

        e.preventDefault(); 
      }
     e.preventDefault();
    },
  
               // Customer methods //

    fetchCustomers(){
      this.$http.get('http://localhost:8888/v2/public/api/customers')
      .then(function (response){
       this.customers = response.data;  
      });
     
    },
    filterBy(list,value){
      value = value.charAt(0).toUpperCase() + value.slice(1);
      return list.filter(function(customer){
         return customer.last_name.indexOf(value) > -1 ;
      })
    }

  },

  created: function() {
    if(this.$route.query.alert){
      this.alert = this.$route.query.alert;
    }
     this.fetchCustomers();
     Bus.$on('afterCreated', ()=> this.fetchCustomers());

  },
  
  components:{
    Alert
  }

  
}
</script>



<style scoped>


</style>

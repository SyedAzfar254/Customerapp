<template>
  <div class="edit container">
  <Alert v-if="alert" v-bind:message="alert"/>
  <h1 class = "page-header"> Edit Customer </h1>
 
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'add',
  data (){
    return {
     
     alert:''
    }
  },
  methods:{

    
  },
  created: function () {
      this.fetchCustomer(this.$route.params.id);
  },
  components:{
      Alert
  }
}
</script>



<style scoped>


</style>

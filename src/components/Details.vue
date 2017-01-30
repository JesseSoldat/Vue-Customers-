<template>
  <div class="details container">
    <router-link to="/">Back</router-link>
    <h1 class="page-header">{{customer.first_name}} {{customer.last_name}}
    	<span class="pull-right">
    		<router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">Edit</router-link>
    		<button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">Delete</button>
    	</span>
    </h1>
    <ul class="list-group">
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-phone"></span>&nbsp;&nbsp;&nbsp;{{customer.phone}}
    	</li>
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-envelope"></span>&nbsp;&nbsp; {{customer.email}}
    	</li>
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
  name: 'details',
  data () {
    return {
      customer: ''
    }
  },
  methods: {
  	fetchCustomer(id){
  		this.$http.get('http://slimapp/api/customer/'+id)
  			.then(function(res){
  				// console.log(res)
  				this.customer = JSON.parse(res.body);
  			});
  	},
  	deleteCustomer(id){
  		this.$http.delete('http://slimapp/api/customer/delete/'+id)
  			.then(function(res){
  				this.$router.push({path: '/'});
  			});
  	}
  },
  created: function(){
  	this.fetchCustomer(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

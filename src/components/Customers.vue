<template>
  <div class="customers container">
    <h1 class="page-header">Manage Customers</h1>
    <input class="form-control" placeholder="Enter Last Name">
    <br>
    <table class="table tabel-striped">
    	<thead>
    		<tr>
    			<th>First Name</th>
    			<th>Last Name</th>
    			<th>Email</th>
    			<th></th>
    		</tr>
    	</thead>
    	<tbody>
    		<tr v-for="customer in customers">
    			<td>{{customer.first_name}}</td>
    			<td>{{customer.last_name}}</td>
    			<td>{{customer.email}}</td>
    		</tr>
    	</tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'customers',
  data () {
    return {
      customers: []
    }
  },
  methods: {
  	fetchCustomers(){
  		this.$http.get('http://slimapp/api/customers')
  			.then(function(response){
  			
  				let res = response.body;
  				// console.log(typeof(res));
  				let resString = res.slice(9);

  				this.customers = JSON.parse(resString);
  			});
  	}
  },
  created: function(){
  	this.fetchCustomers();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

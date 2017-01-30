<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Manage Customers</h1>
    <input class="form-control" placeholder="Enter Last Name" v-model="filterInput">
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
    		<tr v-for="customer in filterBy(customers, filterInput)">
    			<td>{{customer.first_name}}</td>
    			<td>{{customer.last_name}}</td>
    			<td>{{customer.email}}</td>
    			<td><router-link class="btn btn-default" v-bind:to="'/details/'+customer.id">View</router-link></td>
    		</tr>
    	</tbody>
    </table>
  </div>
</template>

<script>
import Alert from './Alert';
export default {
  name: 'customers',
  components: {
    Alert
  },
  data () {
    return {
      customers: [],
      filterInput:'',
      alert: ''
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
  	},
    
    filterBy(list, value){
        value = value.charAt(0).toUpperCase() + value.slice(1);
        console.log(value)
        return list.filter(function(customer){
          return customer.last_name.indexOf(value) > -1;
        });
      }
  },
  created: function(){
  	this.fetchCustomers();
    this.alert = this.$route.query.alert;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

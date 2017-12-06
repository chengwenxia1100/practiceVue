<template>
  <div class="details container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
    	{{custorm.name}}
		<span class="pull-right">
			<router-link class="btn btn-primary" v-bind:to="'/edit/'+ custorm.id">编辑</router-link>
			<button class="btn btn-danger" v-on:click="delectCustorm(custorm.id)">删除</button>
		</span>
    </h1>
    <ul class="list-group">
    	<li class="list-group-item"><span class="glyphicon glyphicon-phone"> {{custorm.phone}}</span></li>
    	<li class="list-group-item"><span class="glyphicon glyphicon-log-out"> {{custorm.email}}</span></li>
    	<li class="list-group-item"><span class="glyphicon glyphicon-fire"> {{custorm.education}}</span></li>
    	<li class="list-group-item"><span class="glyphicon glyphicon-home"> {{custorm.graduationschool}}</span></li>
    	<li class="list-group-item"><span class="glyphicon glyphicon-certificate"> {{custorm.profession}}</span></li>
    	<li class="list-group-item"><span class="glyphicon glyphicon-heart-empty"> {{custorm.profile}}</span></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'custormdetails',
  data () {
    return {
     	custorm:"",
    }
  },
  methods:{
  	fetchCustomers(id){
  		this.$http.get("http://localhost:3000/users/"+id)
  		   .then(function(response){
  			// console.log(response);
  			this.custorm = response.body;
        })
  	},
  	delectCustorm(id){
  		// console.log(id)
  		this.$http.delete("http://localhost:3000/users/"+id)
  		   .then(function(response){
  			this.$router.push({path:'/',query:{alert:"用户删除成功！"}});
        })
  	}
  },
  created(){
  	this.fetchCustomers(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

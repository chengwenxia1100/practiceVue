<template>
  <div class="edit container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h1 class="page-header">添加用户</h1>
    <form v-on:submit="editCustorm">
    		<div class="well">
    			<h4>用户信息</h4>
    			<div class="form-group">
    				<label>姓名</label>
    				<input type="text" class="form-control" placeholder="name" v-model="custorm.name">
    			</div>
    			<div class="form-group">
    				<label>电话</label>
    				<input type="text" class="form-control" placeholder="phone" v-model="custorm.phone">
    			</div>
    			<div class="form-group">
    				<label>邮箱</label>
    				<input type="text" class="form-control" placeholder="email" v-model="custorm.email">
    			</div>
    			<div class="form-group">
    				<label>学历</label>
    				<input type="text" class="form-control" placeholder="education" v-model="custorm.education">
    			</div>
    			<div class="form-group">
    				<label>毕业学校</label>
    				<input type="text" class="form-control" placeholder="graduationschool" v-model="custorm.graduationschool">
    			</div>
    			<div class="form-group">
    				<label>职业</label>
    				<input type="text" class="form-control" placeholder="profession" v-model="custorm.profession">
    			</div>
    			<div class="form-group">
    				<label>个人简介</label>
    				<!-- <input type="text" class="form-control" placeholder="profile" v-model="custorm.profile"> -->
    				<textarea class="form-control" rows="10" v-model="custorm.profile">
    					
    				</textarea>
    			</div>
    			<button type="submit" class="btn btn-primary"> 确认修改</button>
    		</div>
    </form>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'add',
  data () {
    return {
     custorm:{},
     alert:""
    }
  },
  methods:{
    fetchCustomer(id){
      this.$http.get("http://localhost:3000/users/"+ id )
        .then(function(response){
            console.log(response);
            this.custorm = response.body;
        }) 
    },
  	editCustorm(e){
  		if(!this.custorm.name || !this.custorm.phone || !this.custorm.email){
  			//console.log('请添加信息');
        this.alert = "请添加信息";
  		}else{
  			let editCustorm = {
  				name:this.custorm.name,
  				phone:this.custorm.phone,
  				email:this.custorm.email,
  				education:this.custorm.education,
  				graduationschool:this.custorm.graduationschool,
  				profession:this.custorm.profession,
  				profile:this.custorm.profile 				
  			}

  			this.$http.put("http://localhost:3000/users/"+this.$route.params.id,editCustorm)
				.then(function(response){
	  				// alert(response);
	  				this.$router.push({path:"/",query:{alert:"用户信息更新成功！"}});
	        	})
	        e.preventDefault();
  		}
  		e.preventDefault();
  	}
  },
  created(){
    this.fetchCustomer(this.$route.params.id)
  },
  components:{
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

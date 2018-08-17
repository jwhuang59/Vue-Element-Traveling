<template>
    <div id="loading" v-show="loading">
      <div class="loading" v-loading="loading" element-loading-background="rgba(255, 255, 255, 0.8)"></div>

    </div>
</template>
<script>
import Vue from 'vue'

export default {
	data () {
		return {
			loading:false
		}

	},
	mounted () {
		Vue.http.interceptors.push((request, next) =>{ 

		 let TOKEN=sessionStorage.getItem('STORAGE_TOKEN'); 
		 if(TOKEN){ 
		  
		  request.headers.set('TOKEN',TOKEN); 
		 } 
		 this.loading = true
		 
		 next((response) => { 
			this.loading = false
		  
		   return response;
		 }); 
		}); 

	}

}


</script>
<style>
#loading{max-width:450px;width:100%;position:fixed;left:0;right:0;top:0;bottom:0;margin:0 auto;z-index:9999;}

.loading{height:100%;}
.el-loading-spinner .path{stroke:#06c1ae;}

</style>
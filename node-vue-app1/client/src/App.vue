<template>
  <div id="app">
    <NavBar></NavBar>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
    <Footer></Footer>
	<Loading v-show="loading"></Loading>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Landing from './components/Landing.vue'
import Footer from './components/Footer.vue'
import jwt_decode from 'jwt-decode'
import Loading from './components/common/loading.vue'

export default {
  name: 'App',
  components: {
		NavBar,
		Landing,
		Footer,
		Loading
	},
	computed: {
		loading() {
			return this.$store.getters.loading;
		}
	},
	created() {
		if(localStorage.jwtToken){
			const decoded = jwt_decode(localStorage.jwtToken);
			
			//获取当前时间
			const currentTime = Date.now() / 1000;
			//检测token是否过期
			if(decoded.exp < currentTime) {
				// this.$store.dispatch('setIsAuthenticated', false);
				// this.$store.dispatch('setUser', {});
				this.$store.dispatch('clearCurrentState');
				this.$router.push('/login')
			} else {
				//分发actio更改store的state
				this.$store.dispatch('setIsAuthenticated', !this.isEmpty(decoded));
				this.$store.dispatch('setUser', decoded);
			}
			
			
		}
	},
	methods: {
		isEmpty(value){
			return (
				value === undefined ||
				value === null ||
				(typeof value === 'object' && Object.keys(value).length === 0) ||
				(typeof value === 'string' && value.trim().length === 0)
			)
		}
	}
}
</script>

<style>

</style>

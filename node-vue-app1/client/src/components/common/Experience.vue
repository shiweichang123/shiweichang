<template>
		<div>
			<h4 class="mb-2">个人履历</h4>
			<table class="table">
				<thead>
				<tr>
					<th>公司</th>
					<th>职位</th>
					<th>年份</th>
					<th />
				</tr>
				</thead>
				<tbody>
				<tr v-for="exp in experience" :key="exp._id">
					<td>{{exp.company}}</td>
					<td>{{exp.title}}</td>
					<td>
					{{exp.from}} ~ {{exp.to}}
					</td>
					<td>
					<button @click="deleteClick(exp._id)" class="btn btn-danger">
						删除
					</button>
					</td>
				</tr>
				</tbody>
			</table>
		</div>
</template>

<script>
	export default {
		name: 'ExperiEnce',
		data() {
			return {};
		},
		props: {
			experience: Array
		},
		created() {
			console.log(this.experience);
		},
		methods: {
			deleteClick(id){
				//在vue2.0以上版本不能直接在子组件修改,所以在父组件上定义方法
				// this.$axios.delete('api/profile/experience/${id}')
				// .then(res => {
				// 	console.log(ers.data);
				// 	this.experience = res.data.experience;
				// })
				// .catch(err => {
				// 	console.log(err);
				// })
				this.$emit("deleteExperience",id);
			}
		}
	}
</script>

<style>
</style>
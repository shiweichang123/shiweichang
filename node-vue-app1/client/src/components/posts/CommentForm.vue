<template>
	<div class="post-form mb-3">
		<div class="card card-info">
			<div class="card-header bg-info text-white">
				说点啥...
			</div>
			<form @submit.prevent="submit">
				<TextArea 
					name="text"
					placeholder="随便写点啥"
					v-model="text"
					:error="errors.text"
				></TextArea>
				<input type="submit" class="btn btn-dark">
			</form>
			<div class="card-body">
				
			</div>
		</div>
	</div>
</template>

<script>
	import TextArea from '../common/TextAreaGroup.vue'
	export default {
		name: 'CommentForm',
		data() {
			return {
				text:'',
				errors:{}
			};
		},
		props: {
			postId: String
		},
		components: {
			TextArea
		},
		methods: {
			submit() {
				// console.log(this.text);
				const user = this.$store.getters.user;
				
				const newComment = {
					text:this.text,
					name:user.name,
					avatar:user.avatar
				};
				
				//添加评论
				this.$axios.post(`/api/posts/comment/${this.postId}`,newComment)
				.then(res => {
					console.log(res.data);
					this.errors = {};
					this.text = "";
					this.$emit('update');
				})
				.catch(err => {
					this.errors = err.response.data;
				})
			}
		}
	}
</script>

<style>
</style>
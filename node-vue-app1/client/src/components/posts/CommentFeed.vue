<template>
	<div class="commentfeed">
			<!-- Post Item -->
			<div class="card card-body mb-3">
				<div class="row">
					<div class="col-md-2">
						<a href="profile.html">
							<img style="width:150px" class="rounded-circle d-nonse d-md-block" :src="comment.avatar" alt="" />
						</a>
						<br />
						<p class="text-center">{{comment.name}}</p>
					</div>
					<div class="col-md-10">
						<p class="lead">{{comment.text}}</p>
						<button @click="deleteClick(comment._id)" v-if="user != null && user.id == comment.user" type="button" class="btn btn-danger mr-1">
							<i class="fas fa-times" />
						</button>
					</div>
				</div>
			</div>
	</div>
</template>

<script>
	export default {
		name: 'CommentFeed',
		data(){
			return {};
		},
		props: {
			comment: Object,
			postId: String
		},
		computed: {
			user() {
				return this.$store.getters.user;
			}
		},
		methods: {
			deleteClick(id) {
				this.$axios.delete(`/api/posts/comment/${this.postId}/${id}`)
				.then(res => {
					console.log(res.data);
					//删除成功 更新数据
					this.$emit('update');
				})
				.catch(err => {
					console.log(err.response.data);
					console.log(this.postId);
				})
			}
		}
	}
</script>

<style>
</style>
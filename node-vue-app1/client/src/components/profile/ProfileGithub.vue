<template>
	<div>
	<hr />
	<h3 class="mb-4">GitHub仓库信息</h3>
	<div v-for="repo in repos" :key="repo.id" class="card card-body mb-2">
		<div class="row">
			<div class="col-md-6">
				<h4>
					<a :href="repo.html_url" class="text-info" target="_blank">
						{{repo.name}}
					</a>
				</h4>
				<p>{{repo.description}}</p>
			</div>
			<div class="col-md-6">
				<span class="badge badge-info mr-1">
					Stars: {{repo.stargazers_count}}
				</span>
				<span class="badge badge-info mr-1">
					Watchers: {{repo.watchers_count}}
				</span>
				<span class="badge badge-success">
					Forks: {{repo.forks_count}}
				</span>
			</div>
		</div>
	</div>
	</div>
</template>

<script>
	export default {
		name: 'ProfileGithub',
		data() {
			return {
				cliendId:'7e365838fa854abd5862',
				client_secret:'c01c6fae288d03e9d3c18574f478e88dd257aeff',
				count:0,
				sort:'created: desc',
				repos:[]
			};
		},
		props: {
			username: String
		},
		created() {
			//github接口地址
			// https://api.github.com/users/username/repos?per_page=count&sort=sort&client_id=clientId&client_secret=clientSecret
			fetch(`https://api.github.com/users/${this.username}/repos?per_page=${this.count}&sort=${this.sort}&client_id=${this.cliendId}&client_secret=${this.client_secret}`)
			.then(res => res.json())
			.then(data => {
				// console.log(data);
				this.repos = data;
			})
			.catch(err => {
				console.log(err);
			})
		}
	}
</script>

<style>
</style>
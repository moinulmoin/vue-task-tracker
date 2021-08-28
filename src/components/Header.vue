<template>
	<header>
		<h1>{{ title }}</h1>
		<Button
			@btn-click="$emit('toggle-add-task')"
			:text="showAddTask ? 'Close' : 'Add Task'"
			:color="showAddTask ? 'red' : 'royalblue'"
		/>
	</header>
</template>

<script>
	import Button from './Button.vue';

	export default {
		name: 'Header',
		props: {
			title: String,
			showAddTask: Boolean,
		},
		emits: ['toggle-add-task'],
		components: {
			Button,
		},
	};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
</style>

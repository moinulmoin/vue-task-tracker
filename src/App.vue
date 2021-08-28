<template>
	<h1>{{ title }}</h1>
	<div class="container">
		<Header
			title="Task Tracker"
			@toggle-add-task="toggleAddTask"
			:showAddTask="showAddTask"
		/>

		<div v-if="showAddTask">
			<AddTask @add-task="addTask" />
		</div>

		<Tasks
			@delete-task="deleteTask"
			@toggle-task="toggleTask"
			:tasks="tasks"
		/>
	</div>
	<small
		>Coded by <a href="https://github.com/moinulmoin">Moinul Moin</a></small
	>
</template>

<script>
	import Header from './components/Header.vue';
	import Tasks from './components/Tasks.vue';
	import AddTask from './components/AddTask.vue';

	export default {
		name: 'App',
		components: {
			Header,
			Tasks,
			AddTask,
		},
		data() {
			return {
				title: 'Made with Vue',
				tasks: [],
				showAddTask: false,
			};
		},
		methods: {
			addTask(task) {
				this.tasks.push(task);
				// this.tasks = [...this.tasks, task];
			},
			toggleAddTask() {
				this.showAddTask = !this.showAddTask;
			},
			deleteTask(id) {
				if (confirm('Are you sure?')) {
					this.tasks = this.tasks.filter((task) => task.id !== id);
				}
			},
			toggleTask(id) {
				this.tasks = this.tasks.map((task) =>
					task.id === id
						? { ...task, reminder: !task.reminder }
						: task
				);
			},
		},
		created() {
			this.tasks = [
				{
					id: '1',
					text: 'Go for Walk',
					day: 'March 5th at 5.00pm',
					reminder: true,
				},
				{
					id: '2',
					text: 'Complete Project',
					day: 'March 6th at 5:00pm',
					reminder: true,
				},
				{
					id: '3',
					text: 'Take a nap',
					day: 'March 7th at 3:30pm',
					reminder: false,
				},
			];
		},
	};
</script>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Rubik&display=swap');

	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
		font-family: inherit;
	}
	html {
		font-size: 62.5%;
	}
	body {
		font-family: 'Rubik', sans-serif;
		font-size: 1.6rem;
	}
	button {
		border: none;
		cursor: pointer;
		outline: none;
	}
	button:focus {
		box-shadow: none;
		outline: none;
		border: none;
	}

	.container {
		max-width: 500px;
		margin: 30px auto;
		overflow: auto;
		min-height: 300px;
		border: 1px solid royalblue;
		padding: 30px;
		border-radius: 5px;
	}
	.btn {
		display: inline-block;
		background: #000;
		color: #fff;
		border: none;
		padding: 10px 20px;
		margin: 5px;
		border-radius: 5px;
		cursor: pointer;
		text-decoration: none;
		font-size: 15px;
		font-family: inherit;
	}
	.btn:focus {
		outline: none;
	}
	.btn:active {
		transform: scale(0.98);
	}
	.btn-block {
		display: block;
		width: 100%;
	}
</style>

<style scoped>
	h1 {
		margin: 3rem 0;
		font-size: 4rem;
		text-align: center;
	}
	small {
		text-align: center;
		display: block;
		font-size: 1.4rem;
	}
</style>

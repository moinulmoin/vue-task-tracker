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
			async addTask(task) {
				const res = await fetch('/api/tasks', {
					method: 'POST',
					body: JSON.stringify(task),
					headers: {
						'Content-Type': 'application/json',
					},
				});

				const newTask = await res.json();

				this.tasks.push(newTask);
				// this.tasks = [...this.tasks, task];
			},
			toggleAddTask() {
				this.showAddTask = !this.showAddTask;
			},
			async deleteTask(id) {
				if (confirm('Are you sure?')) {
					const res = await fetch(`/api/tasks/${id}`, {
						method: 'DELETE',
					});

					res.status === 200
						? (this.tasks = this.tasks.filter(
								(task) => task.id !== id
						  ))
						: alert('Something went wrong');
				}
			},
			async toggleTask(id) {
				const res = await fetch(`/api/tasks/${id}`);

				const task = await res.json();

				const updatingTask = { ...task, reminder: !task.reminder };

				const res2 = await fetch(`/api/tasks/${id}`, {
					method: 'PUT',
					body: JSON.stringify(updatingTask),
					headers: {
						'Content-Type': 'application/json',
					},
				});

				const updatedTask = await res2.json();

				this.tasks = this.tasks.map((task) =>
					task.id === id
						? { ...task, reminder: updatedTask.reminder }
						: task
				);
			},
			async fetchTasks() {
				const response = await fetch('/api/tasks');
				const tasks = await response.json();
				// console.log(tasks);
				return tasks;
			},
		},
		async created() {
			this.tasks = await this.fetchTasks();
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

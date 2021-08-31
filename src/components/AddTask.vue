<template>
	<form class="add-form" @submit="saveTask">
		<div class="form-control">
			<label>Task</label>
			<input
				type="text"
				name="text"
				placeholder="Add Task"
				v-model="text"
				spellcheck="true"
			/>
		</div>
		<div class="form-control">
			<label>Day & Time</label>
			<input
				type="text"
				name="day"
				placeholder="Add Day & Time"
				v-model="day"
			/>
		</div>
		<div class="form-control form-control-check">
			<input
				type="checkbox"
				name="reminder"
				id="reminder"
				v-model="reminder"
			/>
			<label for="reminder">Set Reminder</label>
		</div>

		<input type="submit" value="Save Task" class="btn btn-block" />
	</form>
</template>

<script>
	export default {
		name: 'AddTask',
		data() {
			return {
				text: '',
				day: '',
				reminder: false,
			};
		},
		methods: {
			saveTask(e) {
				e.preventDefault();

				if (this.text.trim() === '') {
					alert('Add a valid task');
					return;
				}

				const newTask = {
					id: Math.random() * 10000,
					text: this.text,
					day: this.day,
					reminder: this.reminder,
				};

				this.$emit('add-task', newTask);

				this.text = '';
				this.day = '';
				this.reminder = false;
			},
		},
	};
</script>

<style scoped>
	.add-form {
		margin-bottom: 4rem;
	}

	.form-control {
		margin: 2rem 0;
	}

	.form-control label {
		display: block;
	}

	.form-control input[type='text'] {
		width: 100%;
		height: 4rem;
		margin: 0.5rem 0;
		padding: 0.4rem 0.8rem;
		font-size: 1.8rem;
		border: 1px solid black;
	}

	.form-control input[type='checkbox'] {
		margin-right: 0.5rem;
		width: 1.8rem;
		height: 1.8rem;
		border: 1px solid black;
	}

	.form-control-check {
		display: flex;
		align-items: center;
		font-size: 18px;
	}
</style>

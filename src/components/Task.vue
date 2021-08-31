<template>
	<div :class="['task', task.reminder ? 'reminder' : '']">
		<div @click="$emit('toggle-task', task.id)" class="task-details">
			<h3>{{ task.text }}</h3>
			<p>{{ task.day }}</p>
		</div>
		<button @click="$emit('delete-task', task.id)">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				height="25px"
				viewBox="0 0 20 20"
				fill="#FF0000"
			>
				<path
					fill-rule="evenodd"
					d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z"
					clip-rule="evenodd"
				/>
			</svg>
		</button>
	</div>
</template>

<script>
	export default {
		name: 'Task',
		props: {
			task: Object,
		},
	};
</script>

<style scoped>
	.task {
		background: #f4f4f4;
		margin-top: 2rem;
		padding: 1.2rem 2rem;
		cursor: pointer;
		display: flex;
		align-items: center;
		gap: 2rem;
	}
	.task-details {
		flex-grow: 1;
	}
	.task.reminder {
		border-left: 0.5rem solid royalblue;
	}
	.task h3 {
		display: flex;
		align-items: center;
		justify-content: space-between;
		font-size: 1.8rem;
	}
	.task p {
		margin-top: 0.5rem;
		font-size: 1.5rem;
	}
</style>

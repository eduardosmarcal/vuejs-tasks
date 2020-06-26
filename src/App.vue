<template>
	<div id="app">
		<h1>Tasks</h1>
    <TaskProgress :progress="progress" />
    <NewTask @taskAdded="addTask" />
    <TaskGrid
      :tasks="tasks"
      @taskStateChanged="toggleTaskState"
      @taskDeleted="deleteTask" />
	</div>
</template>

<script>
import TaskProgress from './components/TaskProgress.vue'
import NewTask from './components/NewTask.vue'
import TaskGrid from './components/TaskGrid.vue'

export default {
  components: {
    TaskProgress,
    NewTask,
    TaskGrid,
  },
  data() {
    return {
      tasks: [],
    }
  },
  computed: {
    progress() {
      const done = this.tasks.filter(task => task.done).length
      const total = this.tasks.length
      return Math.round(done / total * 100) || 0
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      }
    },
  },
  methods: {
    addTask(newTask) {
      if (!this.tasks.find(task => task.name === newTask.name)) {
        this.tasks.push(newTask)
      }
    },
    toggleTaskState(index) {
      this.tasks[index].done = !this.tasks[index].done
    },
    deleteTask(index) {
      this.tasks.splice(index, 1)
    },
  },
  created() {
    const json = localStorage.getItem('tasks')
    const tasks = JSON.parse(json)
    this.tasks = Array.isArray(tasks) ? tasks : []
  }
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>

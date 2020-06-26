<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <Task
        v-for="(task, index) in tasks"
        :key="task.name"
        :task="task"
        @taskDeleted="$emit('taskDeleted', index)"
        @taskStateChanged="$emit('taskStateChanged', index)" />
    </template>
    <p v-else class="no-task">
      Congrats! You do not have any tasks.
    </p>
  </div>
</template>

<script>
import Task from './Task.vue'

export default {
  components: {
    Task,
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
    taskStateChanged: Function,
    taskDeleted: Function,
  },
}
</script>

<style>
  .task-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .no-task {
    color: #AAA;
    font-size: 1.625rem;
  }
</style>
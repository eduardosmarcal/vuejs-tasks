<template>
  <div class="task" :class="stateClass" @click="$emit('taskStateChanged', task)">
    <span class="close" @click.stop="$emit('taskDeleted', task)">x</span>
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
    taskStateChanged: Function,
    taskDeleted: Function,
  },
  computed: {
    stateClass() {
      return {
        done: this.task.done,
      }
    },
  },
}
</script>

<style>
  .task {
    align-items: center;
    background-color: #F44336;
    border-left: 12px solid #B73229;
    border-radius: 8px;
    box-sizing: border-box;
    cursor: pointer;
    display: flex;
    font-size: 2rem;
    font-weight: 300;
    height: 150px;
    justify-content: center;
    margin: 10px;
    padding: 10px;
    position: relative;
    user-select: none;
    width: 350px;
  }

  .task.done {
    background-color: #4CAF50;
    border-left-color: #0A8F08;
    color: #DDD;
    text-decoration: line-through;
  }

  .task .close {
    background-color: #B73229;
  }

  .task.done .close {
    background-color: #0A8F08;
  }

  .close {
    border-radius: 10px;
    display: flex;
    font-size: .875rem;
    font-weight: 600;
    height: 20px;
    justify-content: center;
    position: absolute;
    right: 10px;
    top: 10px;
    width: 20px;;
  }
</style>
<template>
  <div class="task-progress">
    <span class="progress-value">{{ progress }}%</span>
    <div class="progress-bar" :style="{ width: `${progress}%` }"></div>
  </div>
</template>

<script>
export default {
  props: {
    progress: {
      type: Number,
      default: 0,
    },
  },
}
</script>

<style>
  .task-progress {
    align-items: center;
    border: 1px solid #FFF;
    border-radius: 8px;
    color: #FFF;
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;
    position: relative;
    width: 80%;
  }
  
  .progress-value {
    font-size: 1.5rem;
    z-index: 1;
  }

  .progress-bar {
    align-self: flex-start;
    background-color: #4CAF50;
    border-radius: 8px;
    height: 100%;
    position: absolute;
  }
</style>
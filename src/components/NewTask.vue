<template>
  <div class="new-task">
    <input type="text" class="form-element" placeholder="New Task?" v-model="name" @keydown.enter="add">
    <button type="button" class="form-element" @click="add">+</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
    }
  },
  methods: {
    add() {
      if (this.name.trim() === '') {
        return;
      }
      this.$emit('taskAdded', {
        name: this.name,
        done: false,
      })
      this.name = ''
    }
  },
}
</script>

<style>
  .new-task {
    margin: 35px;
  }

  .form-element {
    border: 1px solid #FFF;
    color: #FFF;
    font-size: 2rem;
    outline: none;
    padding: 5px 10px 8px;
  }

  input.form-element {
    background-color: #FFF2;
    border-bottom-left-radius: 8px;
    border-top-left-radius: 8px;
    width: 500px;
  }

  button.form-element {
    background-color: #2196F3;
    border-bottom-right-radius: 8px;
    border-left: none;
    border-top-right-radius: 8px;
    cursor: pointer;
  }
</style>
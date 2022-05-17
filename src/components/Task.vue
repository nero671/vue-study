<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>
      {{ task.text }}
      <div class="cross" @click="$emit('delete-task', task.id)">
        <span></span>
        <span></span>
      </div>
    </h3>
    <p>{{ task.day }}</p>
  </div>

</template>

<script>
  export default {
    name: 'Task',
    props: {
      task: Object
    },
  }
</script>

<style scoped>
  .task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 5px;
  }

  .task.reminder {
    border-left: 5px solid #41B879;
  }

  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .cross {
    width: 15px;
    cursor: pointer;
    display: inline;
  }

  .cross span {
    background: #000;
    width: inherit;
    height: 3px;
    display: block;
  }

  .cross span:first-child {
    transform: rotate(45deg);
  }

  .cross span:last-child {
    transform: rotate(-45deg) translate(2px, -2px);
  }

</style>

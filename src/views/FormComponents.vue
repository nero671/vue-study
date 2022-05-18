<template>
  <div class="container">
    <HeaderForm @btn-click="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>

    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :key="tasks.id" :tasks="tasks" />
  </div>
</template>

<script>
import HeaderForm from "../components/HeaderForm.vue";
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";
  export default {
    name: 'FormComponents',
    components: {
      HeaderForm,
      Tasks,
      AddTask
    },
    data() {
      return {
        tasks: [],
        showAddTask: false
      }
    },
    methods: {
      toggleAddTask() {
        this.showAddTask = !this.showAddTask;
      },
      addTask(task) {
        this.tasks = [...this.tasks, task]
        console.log(task)
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      },
      toggleReminder(id) {
        this.tasks = this.tasks.map((task) => task.id === id ?
            {...task, reminder: !task.reminder} : task)
      }
    },
    created() {
      this.tasks = [
        {
          id: 1,
          text: 'Doctors Appointment',
          day: 'March 1st at 2:30pm',
          reminder: true
        },
        {
          id: 2,
          text: 'Meeting at work',
          day: 'March 3rd at 1:30pm',
          reminder: true
        },
        {
          id: 3,
          text: 'Food Shopping',
          day: 'March 3rd at 11:00am',
          reminder: false
        },
      ]
    },
  }

</script>

<style scoped lang="scss">

</style>

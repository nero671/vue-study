<template>
  <div class="container">
    <HeaderForm @btn-click="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" @click="fetchTasks" />
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
      async addTask(task) {
        const res = await fetch(`http://localhost:5000/tasks`, {
          method: 'POST',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(task)
        })
        const data = await  res.json();
        this.tasks = [...this.tasks, data]
        console.log(task)
      },
      async deleteTask(id) {
        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: 'DELETE'
        })
        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error deleting task')

      },
      async toggleReminder(id) {
        const taskToToggle = await this.fetchTask(id);
        const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(updTask)
        })

        const data = await res.json();

        this.tasks = this.tasks.map((task) => task.id === id ?
            {...task, reminder: data.reminder} : task)
      },
      async fetchTasks() {
        const response = await fetch(`http://localhost:5000/tasks`);

        const data = await response.json();

        return data
      },
      async fetchTask(id) {
        const response = await fetch(`http://localhost:5000/tasks/${id}`);

        const data = await response.json();

        return data
      }
    },
    async created() {
      this.tasks = await this.fetchTasks();
    },
  }

</script>

<style scoped lang="scss">

</style>

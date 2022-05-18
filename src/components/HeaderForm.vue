 <template>
   <div class="header-form">
     <h1>{{ title }}</h1>
     <Button @click="onClick" @toggle-add-task="$emit('toggle-add-task')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : '#41B879'" />
   </div>
 </template>

 <script>
  import Button from "./Button.vue";
  export default {
    name: 'HeaderForm',
    components: {Button},
    props: {
      title: String,
      showAddTask: Boolean,
    },
    methods: {
      onClick() {
        this.$emit('btn-click')
      }
    }
  }
 </script>

 <style scoped>
 .header-form {
   display: flex;
   justify-content: space-between;
   align-items: center;
   margin-bottom: 20px;
 }

 </style>

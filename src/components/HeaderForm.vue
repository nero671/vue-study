 <template>
   <div class="header-form">
     <h1>{{ title }}</h1>
     <Button @click="onClick()" text="Add Task" color="#41B879" />
   </div>
 </template>

 <script>
  import Button from "./Button.vue";
  export default {
    name: 'HeaderForm',
    components: {Button},
    props: {
      title: String,
    },
    methods: {
      onClick() {
        console.log('click')
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

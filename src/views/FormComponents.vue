<template>
  <div class="form">
    <ul id="example-1">
      <li v-for="item in data.items" :key="item.message" @click="click(item.message)">
        {{ item.message }}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'FormComponents',
    data() {
      return {
        data: {
          items: [
            {message: 'Foo'},
            {message: 'Bar'}
          ]
        }
      }
    },
    methods: {
      click(message) {
        console.log(message)
      }
    },
  }

</script>

<style scoped lang="scss">

</style>

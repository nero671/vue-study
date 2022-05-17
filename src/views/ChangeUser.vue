<template>
  <div class="changeUser">
    <img :src="picture" :class="gender" :alt="`${firstName} ${lastName}`" />
    <h1>{{firstName}} {{lastName}}</h1>
    <h3>age: {{age}}</h3>
    <h3>{{country}}, {{city}}</h3>
    <h3>Email: {{email}}</h3>
    <button @click="getUser()" :class="gender">Get Random User</button>
  </div>
</template>

<script>
export default {
  name: 'changeUser',
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe',
      age: 44,
      country: 'USA',
      city: 'LA',
      email: 'jogn@gmail.com',
      gender: 'male',
      picture: 'https://randomuser.me/api/portraits/men/66.jpg'
    }
  },
  methods: {
    async getUser() {
      const response = await fetch('https://randomuser.me/api/');
      const { results } = await response.json();
      this.firstName = results[0].name.first;
      this.lastName = results[0].name.last;
      this.age = results[0].dob.age;
      this.country = results[0].location.country;
      this.city = results[0].location.city;
      this.email = results[0].email;
      this.gender = results[0].gender;
      this.picture = results[0].picture.large;
    }
  },
}

</script>

<style scoped>

  .changeUser {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 35px;
  }

  img {
    border-radius: 50%;
    object-fit: cover;
  }

  button {
    margin-top: 10px;
    padding: 10px;
    color: #fff;
    font-weight: 700;
    cursor: pointer;
  }

  .male {
    background: steelblue;
    border: 5px solid steelblue;
  }

  .female {
    background: pink;
    border: 5px solid pink;
    color: #333;
  }

</style>

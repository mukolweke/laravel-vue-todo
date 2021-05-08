<template>
  <div class="dashboard">
    <p>Logged In</p>
    <p>Email: {{ email}}</p>

    <div>
      <button @click="logout">Logout</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

axios.defaults.withCredentials = true;
axios.defaults.baseURL = 'http://localhost:8000';

export default {
  name: "Dashboard",

  data(){
    return {
      email: ''
    }
  },

  methods: {
    logout(){
      axios.post('/logout').then(response => {
        this.$router.push({ name: 'Home'})
      }).catch(err => console.log(err))
    }
  },

  mounted() {
    axios.get('/api/user')
    .then(response => {
      this.email = response.data.email
    })
  }
}
</script>

<style scoped>

</style>
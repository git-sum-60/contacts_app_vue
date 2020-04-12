<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-bind:key="contact.id" v-for="contact in contacts">
      <p>first_name: {{ contact.first_name }}</p>
      <p>last_name: {{ contact.last_name }}</p>
      <p>email: {{ contact.email }}</p>
      <p>phone_number: {{ contact.phone }}</p>
      <hr>
      <hr>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      contacts: []
    };
  },
  created: function() {
    console.log('in created home page')
    axios.get('/api/contacts').then(response => {
      console.log(response.data);
      this.contacts = response.data;
    })
  },
  methods: {}
};
</script>

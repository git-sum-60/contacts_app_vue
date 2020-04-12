<template>
  <div class="home">
    <h1>{{ message }}</h1>
    first name: <input type="text" v-model="newContact.firstName">
    last name: <input type="text" v-model="newContact.lastName">
    email: <input type="text" v-model="newContact.email">
    phoneNumber: <input type="text" v-model="newContact.phoneNumber">
    address: <input type="text" v-model="newContact.address">

    <button v-on:click="addContact()">Add new contact</button>
    
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
      contacts: [],
      newContact: {
        firstName: "",
        lastName: "",
        email: "",
        phoneNumber: ""        
      }
    };
  },
  created: function() {
    console.log('in created home page')
    axios.get('/api/contacts').then(response => {
      console.log(response.data);
      this.contacts = response.data;
    })
  },
  methods: {
    addContact: function() {
      console.log('i am adding a contact...')
      console.log(this.newContact.firstName)

      var params = {
        first_name: this.newContact.firstName,
        last_name: this.newContact.lastName,
        email: this.newContact.email,
        phone_number: this.newContact.phoneNumber,
        address: this.newContact.address
      }

      axios.post('/api/contacts', params).then(response => {
        console.log(response.data);
      })
    }
  }
};
</script>

<template>
  <div class="home">
    <h1>Vue.js People App</h1>
    <div>
      Name: <input v-model="newPerson.name">
      Bio: <input v-model="newPerson.bio">
      <button v-on:click="addPerson()">Add Person</button>
    </div>

    <div>
      <h4>Number of people: {{ people.length }}</h4>
    </div>
    
    <div v-for="person in people" >
      <h2 @click="toggleBio(person)">{{ person.name }}</h2>
      <div v-bind:class="{strike: person.bioVisible}">
        <h3>{{ person.bio }}</h3>
        <button @click="removePerson(person)">Remove Person</button>
      </div>
    </div>    
  </div>
</template>

<style>
  body {
    background-color: lightblue;
  }

  .strike {
    text-decoration: line-through;
  }
</style>

<script>
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      people: [
        {
          name: "Kamina",
          bio: "From Gurren Laggan",
          bioVisible: true
        },
        {
          name: "Naruto",
          bio: "From Naruto",
          bioVisible: true
        },
        {
          name: "Ichigo",
          bio: "From Bleach",
          bioVisible: true
        }
      ],
      newPerson: {name: "", bio: "", bioVisible: true}
    };
  },
  created: function() {},
  methods: {
    addPerson: function() {
      if (this.newPerson.name && this.newPerson.bio) {
        this.people.push(this.newPerson)
        this.newPerson = {name: "", bio: "", bioVisible:true}
      }
    },
    toggleBio: function(inputPerson) {
        inputPerson.bioVisible = !inputPerson.bioVisible
    },
    removePerson: function(inputPerson) {
      var index = this.people.indexOf(inputPerson);
      this.people.splice(index, 1)
    }
  }, 
  computed: {}
};
</script>

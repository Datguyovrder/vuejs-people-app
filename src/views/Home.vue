<template>
  <div class="home">
    <h1>Vue.js People App</h1>
    <div>
      Name: <input v-model="newPerson.name">
      Bio: <input v-model="newPerson.bio">
      <button v-onLclick="addPerson()">Add Person</button>
    </div>

    <div v-for="person in people" >
      <h2>{{ person.name }}</h2>
      <p>{{ person.bio }}</p>
    </div>


  </div>
</template>

<style>
  body {
    background-color: lightblue;
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
      
    }
  }, computed: {}
};
</script>

<template>
  <div class="home">
    <h1>Interesting People</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
    <div>
      Name: <input v-model="newPerson.name">  
      Bio: <input v-model="newPerson.bio">
      <button v-on:click="addPerson()">Add Person</button>
    </div>

    <div>
      <h4>Total Number of People: {{ people.length }}</h4>
    </div>

    <div>
      Search: <input v-model="nameFilter" list="names">
      <datalist id="names">
        <option v-for="person in people">{{ person.name }}</option>
      </datalist>
    </div>

    <div>
      <button @click="setSortAttribute('name')">Sort by Name</button>
      <button @click="setSortAttribute('bio')">Sort by Bio</button>
    </div>

    <div v-for="person in orderBy(filterBy(people, nameFilter, 'name'), sortAttribute, sortOrder)">
      <h2 @click="toggleBio(person)">{{ person.name }}</h2>
      <div v-if="person.bioVisible">
        <h3>{{ person.bio }}</h3>
        <button @click="deletePerson(person)">Delete</button>
      </div>
    </div>
  </div>
</template>

<style>
.strike {
  text-decoration: line-through;
}
</style>

<script>
var axios = require('axios');
export default {
  data: function() {
    return {
      people: [],
      newPerson: {name: "", bio: "", bioVisible: false},
      errors: [],
      nameFilter: "",
      sortAttribute: 'name',
      sortOrder: 1
    };
  },
  created: function() {
    axios
    .get("http://localhost:3000/api/people")
    .then(response => {
      this.people = response.data;
    });
  },
  methods: {
    toggleBio: function(inputPerson) {
      inputPerson.bioVisible = !inputPerson.bioVisible;
    },
    addPerson: function() {
      this.errors = [];
      var params = {
                    name: this.newPerson.name,
                    bio: this.newPerson.bio
                    };
      axios
      .post("http://localhost:3000/api/people", params)
      .then(response => {
        this.people.push(response.data);
        this.newPerson = {name: "", bio: "", bioVisible: false};
      })
      .catch(error => {
        this.errors = error.response.data.errors;
      });
    },
    deletePerson: function(inputPerson) {
      var index = this.people.indexOf(inputPerson);
      this.people.splice(index, 1);
    },
    setSortAttribute: function(inputAttribute) {
      if (this.sortAttribute === inputAttribute) {
        this.sortOrder = this.sortOrder * -1;
      } else {
        this.sortOrder = 1;
      }
      this.sortAttribute = inputAttribute;
    }
  },
  computed: {}
};
</script>

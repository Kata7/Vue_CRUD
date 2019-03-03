<template>
  <div id="app">
    <Navbar />
    <button v-on:click="this.toggleCompose">Add Joke</button>
    <AddForm v-if="compose"/>
    <JokeEdit v-for="joke in data" v-bind:key="joke.id" v-bind:joke="joke"/>
    
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import AddForm from './components/AddForm.vue'
import JokeEdit from './components/JokeEdit.vue'

export default {
  name: 'app',
  components: {
    Navbar,
    AddForm,
    JokeEdit
  },
  data() {
    return {
      compose: false,
      data: [],
      url: "",
      joke: ""
    }
  },
  methods: {
    toggleCompose() {
      this.compose = !this.compose
    },
    getData() {
      fetch('http://silly-dilf.herokuapp.com')
      .then(response => response.json())
      .then(responseJSON => this.data = responseJSON)
    }
  },
  created: function() {
    this.getData()
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

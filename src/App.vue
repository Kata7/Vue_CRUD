<template>
  <div id="app">
    <Navbar />
    <button 
      v-if="!compose" 
      v-on:click="this.toggleCompose">ADD JOKE</button>
    <AddForm 
      v-if="compose"
      v-on:newJokeSubmit="this.submitClicked"
      v-on:updateAddJoke="joke=$event"
      v-on:updateAddURL="url=$event"
      />
    <JokeEdit
      v-for="joke in data"
      v-bind:key="joke.id" 
      v-bind:joke="joke"
      v-on:delete="deleteJoke($event)"
    />
    
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
      joke: "",
      edit: {
        id: "",
        joke: "",
        url: ""
      }
    }
  },
  methods: {
    getData() {
      fetch('http://silly-dilf.herokuapp.com')
      .then(response => response.json())
      .then(responseJSON => {
        return this.data = responseJSON
        })
    },
    toggleCompose() {
      this.compose = !this.compose
    },
    addJoke() {
      const sendObject = {
        id: "unk",
        text: this.joke,
        url: this.url
      }
      fetch('http://silly-dilf.herokuapp.com', {
        method: 'POST',
        body: JSON.stringify(sendObject),
        headers:{
          'Content-Type': 'application/json'
        }
      })
      .then(res => console.log('joke added'))
      this.data.push(sendObject)
    },
    submitClicked() {
      this.toggleCompose()
      this.addJoke()
    },
    deleteJoke(id) {
      const sendObject = {
        id: id,
        text: "",
        url: ""
      }
      fetch('http://silly-dilf.herokuapp.com', {
        method: 'DELETE',
        body: JSON.stringify(sendObject),
        headers:{
          'Content-Type': 'application/json'
        }
      })
      .then(res => console.log('joke removed'))
    }
  },
  created: function() {
    this.getData()
  }
}
</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  button {
    width: 100%;
    border: none;
    background: blue;
    color: white;
    margin: 5px 0px;
    padding: 5px;
    opacity: 0.8;
  }
</style>

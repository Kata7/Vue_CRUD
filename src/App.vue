<template>
  <div id="app">
    <Navbar />
    <button 
      v-if="!compose" 
      v-on:click="toggleCompose">ADD JOKE</button>
    <AddForm 
      v-if="compose"
      v-on:newJokeSubmit="submitClicked"
      v-on:updateAddJoke="joke=$event"
      v-on:updateAddURL="url=$event"
      />
    <JokeEdit
      v-for="joke in data"
      v-bind:key="joke.id" 
      v-bind:joke="joke"
      v-on:delete="deleteJoke($event)"
      v-on:editJokeText="edit.id=$event.id, edit.joke=$event.joke, edit.url=edit.url"
      v-on:editJokeUrl="edit.id=$event.id, edit.url=$event.url, edit.joke=edit.joke"
      v-on:editJoke="editJoke"
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
      if (this.joke !== "" && this.url !== "") {
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

        // Add joke locally
        this.data.push(sendObject)
      }
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

      // Remove joke locally
      this.data = this.data.filter(joke => joke.id !== id)
    },
    editJoke() {
      if (this.edit.id !== "") {
        if (this.edit.joke === "") {
          this.edit.joke = this.data.filter(joke => joke.id === this.edit.id)[0].text
        }
        if (this.edit.url === "") {
          this.edit.url = this.data.filter(joke => joke.id === this.edit.id)[0].url
        }
        const sendObject = {
          id: this.edit.id,
          text: this.edit.joke,
          url: this.edit.url
        }
        fetch('http://silly-dilf.herokuapp.com', {
          method: 'PATCH',
          body: JSON.stringify(sendObject),
          headers:{
            'Content-Type': 'application/json'
          }
        })
        .then(res => console.log('joke updated'))
      }
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

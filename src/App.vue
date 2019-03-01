<template>
  <div id="app">
    <Navbar />
    <AddForm v-if="compose"/>
    <JokeEdit />
    
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
      compose: false
    }
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

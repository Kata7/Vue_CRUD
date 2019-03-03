<template>
  <div class="joke-container">
    <div class="ID">
      ID: {{joke.id}}
    </div>
    <div class="inputs">
      <input v-on:input="$emit('editJokeText', {id: joke.id, joke: $event.target.value})" v-bind:value="joke.text">
      <input v-on:input="$emit('editJokeUrl', {id: joke.id, url: $event.target.value})" v-bind:value="joke.url">
    </div>
    <div class="buttons">
      <button v-on:click="$emit('editJoke')" class="edit">SAVE</button>
      <button v-on:click="$emit('delete', joke.id)" class="delete">DELETE</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JokeEdit',
  props: {
    joke: Object,
    updateJoke: Function
  }
}
</script>

<style scoped>
  .joke-container {
    display: flex;
    flex-direction: row;
    border: 1px solid black;
    margin: 0px 0px 10px 0px;
    padding: 7px;
    min-width: 600px;
  }

  .ID {
    display: flex;
    width: 10%;
    flex-direction: column;
    align-content: center;
    justify-content: center;
  }

  .inputs {
    display: flex;
    flex-direction: column;
    width: 80%;
  }

  .buttons {
    display: flex;
    flex-direction: column;
    width: 10%;
  }

  button {
    color: white;
    padding: 3px;
    margin: 0px;
    border: none;
    opacity: 0.8;
  }
  .edit {
    background: green;
  }

  .delete {
    background: red;
  }

</style>

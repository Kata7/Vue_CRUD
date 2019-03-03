<template>
  <div class="joke-container">
    <div class="inputs">
      <input v-bind:value="joke.text"></input>
      <input v-bind:value="joke.url"></input>
    </div>
    <div class="buttons">
      <button>EDIT</button>
      <button>DELTE</button>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'JokeEdit',
  props: {
    joke: Object
  }
  
}
</script>

<style scoped>
  .joke-container {
    display: flex;
    flex-direction: row;
    border: 1px solid black;
    margin: 0px 0px 10px 0px;
    padding: 5px;
  }

  .inputs {
    display: flex;
    flex-direction: column;
    width: 90%;;
  }

  .buttons {
    display: flex;
    flex-direction: column;
    width: 10%;
  }

</style>


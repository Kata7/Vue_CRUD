<template>
  <div class='inputDiv'>
    <input v-on:input="$emit('updateAddJoke', $event.target.value)" placeholder='JOKE'></input>
    <input v-on:input="$emit('updateAddURL', $event.target.value)" placeholder='URL'></input>
    <button v-on:click="$emit('newJokeSubmit')">SUBMIT</button>
  </div>
  
</template>

<script>
export default {
  name: 'AddForm',
  props: {}
  
}
</script>

<style scoped>
  .inputDiv {
    border: 1px solid black;
    margin: 5px 0px;
    padding: 5px;
    display: flex;
    flex-direction: column;
    min-width: 600px;
  }

  button {
    border: none;
    margin: 5px 0px 0px 0px;
    padding: 5px;
    background: blue;
    color: white;
    opacity: 0.8;
  }

</style>


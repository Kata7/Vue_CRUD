<template>
  <div class='inputDiv'>
    <input placeholder='JOKE'></input>
    <input placeholder='URL'></input>
    <button>SUBMIT</button>
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


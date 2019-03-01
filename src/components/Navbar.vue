<template>
  <div class='navbar'>
    <div class=title-container>
      <h1 class='title'>Silly-Dilf.com</h1>
    </div>
    <div class='link-container'>
      <ul class='links'>
        <li class='button'><a href='#'>Link 1</a></li>
        <li class='button'><a href='#'>Link 2</a></li>
      </ul>
    </div>
  </div> 
</template>

<script>
export default {
  name: 'Navbar',
  props: {}
  
}
</script>

<style scoped>
  .navbar {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    border: 2px solid black;
    align-content: center;
  }

  .title-container {
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .title {
    margin: 0px 0px 0px 10px;
  }

  .link-container {
    display: flex;
    flex-direction: row;
    align-content: center;
    margin: 0px 10px 0px 0px;
  }

  .links {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    list-style: none;
  }

  .button {
    border: 2px solid black;
    padding: 5px 10px;
    margin: 0px 5px;
  }

  a {
    text-decoration: none;
    color: inherit;
  }

</style>


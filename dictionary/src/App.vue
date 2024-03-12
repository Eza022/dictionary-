<template>
  <form @submit.prevent="getDefinitions()">
    <input placeholder="myWord" type = 'text'id="word"/> 
    <button type="submit"> Get definition</button>
  </form>
  <div id="app">
    
  </div>
</template>

<script>

export default {
  name: 'App',
 
  }

</script>

<style>


</style>

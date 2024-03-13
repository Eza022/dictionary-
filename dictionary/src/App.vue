<template>
  <div>
  <form @submit.prevent="getDefinitions()">
    <input placeholder="myWord" type = "text" id="word" v-model="word" /> 
    <button type="submit"> Get definition</button>
  </form>
  <p v-if="!validQuery"> The word you put doesn't exist</p>
  <div v-for="definition in definitionsArray" :key="definition">{{ definition }}</div>
  </div>
</template>

<script>
import axios from "axios";
import { ref } from "vue";

export default {
  name: "App",

  setup(){
    let validQuery= ref(true);
    const definitionsArray = ref ([]);
    const word =ref ("");

    async function getDefinitions(){
      definitionsArray.value.splice(0, definitionsArray.value.length);

      try{
      const url ="https://api.dictionaryapi.dev/api/v2/entries/en/" + word.value;

      const {data} = await axios.get(url);


      data.map(({meanings})=>{
        meanings.map(({definitions})=>{
          definitions.forEach(({definition})=>{
            if (typeof definition ==="string" )
            definitionsArray.value.push(definition);
          });

        });
      });
    } catch (error){
      validQuery.value = false;
    }
  }
    return{ validQuery, definitionsArray, word, getDefinitions};
  }
 
  }

</script>

<style>


</style>

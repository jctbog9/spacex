<template>
  <div>
    <h2>{{message}}</h2>
    <nuxt-link :to="'/flashcards'">
      <button>Go To Flashcards</button>
    </nuxt-link>
    <ul>
      <li v-for="launch in launches" v-bind:key="launch.flight_number">
        <nuxt-link :to="`launches/${launch.flight_number}`">{{launch.mission_name}}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return { 
        message: 'Welcome! Here you can view all SpaceX launches!',
        launches: []
      }
    },
    methods: {
      useFetch: async function () {
        const { data } = await axios.get('https://api.spacexdata.com/v3/launches')
        this.launches = data
      }
    },
    beforeMount(){
      this.useFetch()
    }
  }
</script>

<style>
  .red {
    background-color: red;
  }
</style>

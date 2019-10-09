<template>
  <div>
    <div>{{message}}</div>
    <button v-on:click="useFetch()">Get Latest Launch</button>
    <div v-if="mission_name">Name: {{mission_name}}</div>
    <div v-if="launch_year">Year: {{launch_year}}</div>
    <div v-if="launch_success">It was a success!</div>
      <div>
        <button v-on:click="clearLaunch()">Clear Launch</button>
      </div>
      <div v-if="mission_name">
        <button class="red" v-on:click="setFailure()">Declare Failure</button>
      </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return { 
        message: 'SpaceX- Latest Launch Info!',
        mission_name: undefined,
        launch_year: undefined,
        launch_success: false
      }
    },
    methods: {
      clearLaunch: function () {
        this.mission_name = undefined
        this.launch_year = undefined
        this.launch_success = false
      },
      setFailure: function () {
        this.launch_success = false
      },
      useFetch: async function () {
        const { data } = await axios.get('https://api.spacexdata.com/v3/launches/latest')
        this.mission_name = data.mission_name
        this.launch_year = data.launch_year
        this.launch_success = data.launch_success
      }
    }
  }
</script>

<style>
  .red {
    background-color: red;
  }
</style>

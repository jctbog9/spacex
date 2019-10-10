<template>
  <div v-if="launch">
    <p v-if="launch.mission_name">{{launch.mission_name}}</p>
    <p v-if="launch.launch_year">Year: {{launch.launch_year}}</p>
    <p v-if="launch.flight_number">Flight Number: {{launch.flight_number}}</p>
    <p v-if="launch.details">{{launch.details}}</p>
  </div>
</template>

<script>
import axios from  'axios'

export default {
  data() {
    return {
      id: this.$route.params.id,
      launch: {
        mission_name: undefined,
        launch_year: undefined,
        details: undefined,
        flight_number: undefined
      }
    }
  },
  methods: {
    useFetch: async function () {
      const { data } = await axios.get(`https://api.spacexdata.com/v3/launches/${this.id}`)
      this.launch.mission_name = data.mission_name
      this.launch.launch_year = data.launch_year
      this.launch.details = data.details
      this.launch.flight_number = data.flight_number
    }
  },
  beforeMount(){
    this.useFetch()
  }
}

</script>

<style>

</style>
<template>
  <div>
    Flashcards Page
    <p v-if="flashcards && flashcardFront">Mission: {{currentFlashcard.mission_name}}</p>
    <div v-if="flashcards && !flashcardFront">
      <p>Flight: {{currentFlashcard.flight_number}}</p>
      <p>Description: {{currentFlashcard.details}}</p>
    </div>
    <p>Card {{counter + 1}}</p>
    <button v-on:click="decrementFlashcard">Previous</button>
    <button v-on:click="flipFlashcard">{{showButtonText}}</button>
    <button v-on:click="incrementFlashcard">Next</button>
  </div>
</template>

<script>
import axios from 'axios'

  export default {
    data() {
      return { 
        message: 'Flashcards!',
        flashcards: [],
        counter: undefined,
        currentFlashcard: {},
        flashcardFront: true,
        showButtonText: 'Show Answer'
      }
    },
    methods: {
      useFetch: async function () {
        const { data } = await axios.get('https://api.spacexdata.com/v3/launches')
        this.flashcards = data.filter(launch => launch.details && launch.mission_name && launch.flight_number && launch.launch_year)
        this.counter = Math.floor(Math.random() * this.flashcards.length)
        this.currentFlashcard = this.flashcards[this.counter]
      },
      incrementFlashcard: function () {
        this.counter < this.flashcards.length - 1 ? this.counter ++ : this.counter = 0
        this.currentFlashcard = this.flashcards[this.counter]
      },
      decrementFlashcard: function () {
        this.counter > 0 ? this.counter -- : this.counter = this.flashcards.length - 1
        this.currentFlashcard = this.flashcards[this.counter]
      },
      flipFlashcard: function () {
        this.flashcardFront = !this.flashcardFront
        this.showButtonText === 'Show Answer' ? this.showButtonText = 'Show Question' : this.showButtonText = 'Show Answer'
      }
    },
    beforeMount(){
      this.useFetch()
    }
  }
</script>

<style>

</style>
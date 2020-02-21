<template>
  <div id="app">
    <HeaderBar />
    <Filters
      :status="filterOptions.status"
      :gender="filterOptions.gender"
      v-on:updateSelectedStatus="receiveSelectedStatus"
      v-on:updateSelectedGender="receiveSelectedGender"
    />
    <CharacterList :characters="characters" />
  </div>
</template>

<script>
import HeaderBar from './components/HeaderBar.vue'
import Filters from './components/Filters.vue'
import CharacterList from './components/CharacterList.vue'

export default {
  name: 'App',
  components: {
    HeaderBar,
    Filters,
    CharacterList
  },
  data() {
    return {
      filterOptions: {
        status: ['Alive', 'Dead', 'unknown'],
        gender: ['Female', 'Male', 'Genderless', 'unknown']
      },
      characters: [
        {
          "id": 1,
          "name": "Rick Sanchez",
          "status": "Alive",
          "species": "Human",
          "type": "",
          "gender": "Male",
          "origin": {
            "name": "Earth",
            "url": "https://rickandmortyapi.com/api/location/1"
          },
          "location": {
            "name": "Earth",
            "url": "https://rickandmortyapi.com/api/location/20"
          },
          "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
          "episode": [
            "https://rickandmortyapi.com/api/episode/1",
            "https://rickandmortyapi.com/api/episode/2"
          ],
          "url": "https://rickandmortyapi.com/api/character/1",
          "created": "2017-11-04T18:48:46.250Z"
        }
      ],
      showStatus: null,
      showGender: null
    }
  },
  methods: {
    receiveSelectedStatus: function (status) {
      console.log('Received selected status', status)
      this.showStatus = status
    },
    receiveSelectedGender: function (gender) {
      console.log('Received selected gender', gender)
      this.showGender = gender
    }
  }
}
</script>

<style>
</style>

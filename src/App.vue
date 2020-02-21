<template>
  <div id="app">
    <HeaderBar />
    <Filters
      :status="filterOptions.status"
      :gender="filterOptions.gender"
      v-on:updateSelectedStatus="receiveSelectedStatus"
      v-on:updateSelectedGender="receiveSelectedGender"
    />
    <CharacterList :characters="renderedCharacters" />
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
      characters: [],
      visibleStatus: ['Alive', 'Dead', 'unknown'],
      visibleGenders: ['Female', 'Male', 'Genderless', 'unknown']
    }
  },
  computed: {
    renderedCharacters: function () {
      return this.characters.filter(character => {
        return this.visibleStatus.includes(character.status) && this.visibleGenders.includes(character.gender)
      })
    }
  },
  methods: {
    getCharacters: async function (url) {
      const response = await fetch(url)
      const json = await response.json()
      this.characters = json.results
    },
    receiveSelectedStatus: function (status) {
      console.log('Received selected status', status)
      this.visibleStatus = status
    },
    receiveSelectedGender: function (genders) {
      console.log('Received selected genders', genders)
      this.visibleGenders = genders
    }
  },
  mounted() {
    this.getCharacters('https://rickandmortyapi.com/api/character/')
  }
}
</script>

<style>
</style>

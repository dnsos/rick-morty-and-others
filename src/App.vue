<template>
  <div id="app">
    <HeaderBar />
    <Filters
      :status="filterOptions.status"
      :gender="filterOptions.gender"
      v-on:updateSelectedStatus="receiveSelectedStatus"
      v-on:updateSelectedGender="receiveSelectedGender"
    />
    <CharacterList />
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

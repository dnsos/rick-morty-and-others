<template>
  <div id="app">
    <HeaderBar />
    <Filters />
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
  }
}
</script>

<style>
</style>

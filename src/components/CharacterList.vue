<template>
  <main class="character-list">
    <h2>Character list</h2>
    <ul>
      <li><Character /></li>
    </ul>
  </main>
</template>

<script>
import Character from './Character.vue'
export default {
  name: 'CharacterList',
  components: {
    Character
  }
}
</script>

<style scoped>
</style>

<template>
  <section class="character-list">
    <h2>Character list</h2>
    <ul>
      <li v-for="(character, index) in characters" v-bind:key="index">
        <Character :characterDetails="character" />
      </li>
    </ul>
  </section>
</template>

<script>
import Character from './Character.vue'

export default {
  name: 'CharacterList',
  components: {
    Character
  },
  props: {
    characters: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.character-list {
  margin-top: var(--grid-spacing);
}
li {
  margin-top: var(--grid-spacing);
}
</style>

<template>
  <section class="wrapper-character-list">
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
.wrapper-character-list {
  margin-top: var(--grid-spacing);
}

ul {
  list-style: none;
  padding: 0;
  display: grid;
  grid-gap: var(--grid-spacing);
  gap: var(--grid-spacing);
  grid-template-columns: repeat(3, 1fr);
}

@media screen and (max-width: 650px) {
  ul {
    grid-template-columns: repeat(2, 1fr);
  }
}

li {
  margin-top: var(--grid-spacing);
}
</style>

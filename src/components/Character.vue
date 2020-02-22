<template>
  <article
    :class="isExtended ? 'character-expanded' : ''"
    v-on:click="toggleExtendedInfo"
  >
    <div class="info-default">
      <img
        :src="characterDetails.image"
        :alt="`Image of ${characterDetails.name}`"
        :class="characterDetails.status === 'Dead' ? 'dead' : ''"
      >
      <h3>{{ characterDetails.name }} <span>| #{{ characterDetails.id }}</span></h3>
      <span>{{ characterDetails.species }} <span v-if="characterDetails.type">{{ characterDetails.type }}</span> </span>
    </div>
    <div
      v-if="isExtended"
      class="info-extended"
    >
      <dl>
        <dt>Status:</dt>
        <dd>{{ characterDetails.status }}</dd>
        <dt>Gender:</dt>
        <dd>{{ characterDetails.gender }}</dd>
        <dt>Origin:</dt>
        <dd>{{ characterDetails.origin.name }}</dd>
        <dt>Last Location:</dt>
        <dd>{{ characterDetails.location.name }}</dd>
      </dl>
    </div>
  </article>
</template>

<script>
export default {
  name: 'Character',
  props: {
    characterDetails: {
      type: Object,
      required: true,
      validator: function (value) {

        const necessaryKeys = ['id', 'name', 'image', 'species', 'type', 'status', 'gender', 'origin', 'location']
        const propKeys = Object.keys(value)
        
        const isIncludedInPropKeys = (currentKey) => propKeys.includes(currentKey)
        
        return necessaryKeys.every(isIncludedInPropKeys)
      }
    }
  },
  data() {
    return {
      isExtended: false
    }
  },
  methods: {
    toggleExtendedInfo: function () {
      this.isExtended = !this.isExtended
    }
  }
}
</script>

<style scoped>
article {
  padding: var(--grid-spacing);
  text-align: center;
  border: 2px solid transparent;
  cursor: pointer;
}

article:hover {
  border-color: var(--color-primary);
}

.character-expanded {
  background-color: var(--color-background);
  border-color: var(--color-primary);
}

.info-default {
  text-align: center;
}

img {
  width: 100%;
  max-width: 300px;
  border-radius: 50%;
}

dt {
  font-size: var(--font-size-small);
}

dd {
  margin: 0;
  font-weight: bold;
}
</style>

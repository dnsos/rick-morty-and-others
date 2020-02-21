<template>
  <article>
    <div class="info-default">
      <h3>{{ characterDetails.name }}</h3>
      <img :src="characterDetails.image" alt="Character Image">
      <dl>
        <dt>ID</dt>
        <dd>{{ characterDetails.id }}</dd>
        <dt>Species</dt>
        <dd>{{ characterDetails.species }}</dd>
        <dd v-if="characterDetails.type">{{ characterDetails.type }}</dd>
      </dl>
    </div>
    <button v-on:click="toggleExtendedInfo">{{ isExtended ? 'Hide' : 'Show' }} details</button>
    <div
      v-if="isExtended"
      class="info-extended"
    >
      <h4>Extended info</h4>
      <dl>
        <dt>Status</dt>
        <dd>{{ characterDetails.status }}</dd>
        <dt>Gender</dt>
        <dd>{{ characterDetails.gender }}</dd>
        <dt>Origin</dt>
        <dd>{{ characterDetails.origin.name }}</dd>
        <dt>Last Location</dt>
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
      required: true
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
</style>

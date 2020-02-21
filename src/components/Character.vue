<template>
  <article>
    <div class="info-default">
      <h3>Name of character</h3>
      <img src="" alt="Character Image">
      <dl>
        <dt>ID</dt>
        <dd>12345</dd>
        <dt>Species</dt>
        <dd>Human</dd>
        <dd>Subtype (if exists)</dd>
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
        <dd>Alive</dd>
        <dt>Gender</dt>
        <dd>Unknown</dd>
        <dt>Origin</dt>
        <dd>Earth</dd>
        <dt>Last Location</dt>
        <dd>Earth</dd>
      </dl>
    </div>
  </article>
</template>

<script>
export default {
  name: 'Character',
  data() {
    return {
      isExtended: true
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

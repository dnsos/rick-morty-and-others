<template>
  <section class="filters">
    <h2>Filters</h2>
    <fieldset>
      <legend>Show status</legend>
      <div v-for="(status, index) in status" :key="index">
        <input
          type="checkbox"
          :id="`status-${status}`"
          :value="status"
          v-model="selectedStatus"
        >
        <label :for="`status-${status}`">{{ status }}</label>
      </div>
    </fieldset>
    <fieldset>
      <legend>Show genders</legend>
      <div v-for="(gender, index) in gender" :key="index">
        <input
          type="checkbox"
          :id="`gender-${gender}`"
          :value="gender"
          v-model="selectedGender"
        >
        <label :for="`gender-${gender}`">{{ gender }}</label>
      </div>
    </fieldset>
  </section>
</template>

<script>
export default {
  name: 'Filters',
  props: {
    status: {
      type: Array,
      default: function () {
        return ['Alive', 'Dead', 'unknown']
      }
    },
    gender: {
      type: Array,
      default: function () {
        return ['Female', 'Male', 'Genderless', 'unknown']
      }
    }
  },
  data() {
    return {
      selectedStatus: this.status,
      selectedGender: this.gender
    }
  },
  watch: {
    selectedStatus: function () {
      this.$emit('updateSelectedStatus', this.selectedStatus)
    },
    selectedGender: function () {
      this.$emit('updateSelectedGender', this.selectedGender)
    }
  }
}
</script>

<style scoped>
.filters, fieldset {
  margin-top: var(--grid-spacing);
}
</style>

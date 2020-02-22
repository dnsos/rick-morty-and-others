<template>
  <section class="filters">
    <h2>Refine results</h2>
    <fieldset>
      <legend>Filter by status:</legend>
      <div
        v-for="(status, index) in status"
        :key="index"
        class="wrapper-checkbox"
        :class="selectedStatus.includes(status) ? 'selected' : ''"
      >
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
      <legend>Filter by gender:</legend>
      <div
        v-for="(gender, index) in gender"
        :key="index"
        class="wrapper-checkbox"
        :class="selectedGender.includes(gender) ? 'selected' : ''"
      >
        <input
          type="checkbox"
          :id="`gender-${gender}`"
          :value="gender"
          v-model="selectedGender"
        >
        <label :for="`gender-${gender}`">{{ gender }}</label>
      </div>
    </fieldset>
    <div class="counter">
      {{ counts.total }} characters in total, {{ counts.page }} on this page, {{ counts.matching }} matching your filters.
    </div>
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
    },
    counts: {
      type: Object,
      required: true,
      validator: function (value) {
        const necessaryKeys = ['total', 'page', 'matching']
        const propKeys = Object.keys(value)
        
        const isIncludedInPropKeys = (currentKey) => propKeys.includes(currentKey)
        
        return necessaryKeys.every(isIncludedInPropKeys)
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
.filters {
  margin-top: var(--grid-spacing);
}

fieldset {
  padding: 0;
  margin: var(--grid-spacing) 0 0;
  border: none;
}

legend {
  font-size: var(--font-size-small);
}

.wrapper-checkbox {
  display: inline-block;
  margin-right: 1rem;
  background-color: var(--color-background);
  border: 2px solid transparent;
}

.wrapper-checkbox:hover {
  border-color: var(--color-primary);
}

input[type=checkbox] { display: none; }

label {
  width: 100%;
  height: 100%;
  padding: .6rem 1.2rem;
  cursor: pointer;
}

.selected {
  color: white;
  background-color: var(--color-secondary);
}

.counter {
  margin-top: var(--grid-spacing);
}
</style>

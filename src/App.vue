<template>
  <div id="app">
    <section class="grid-sidebar">
      <div class="wrapper-sidebar">
        <HeaderBar />
        <Filters
          :status="filterOptions.status"
          :gender="filterOptions.gender"
          :counts="{ ...counts, matching: noOfMatchingCharacters }"
          v-on:updateSelectedStatus="receiveSelectedStatus"
          v-on:updateSelectedGender="receiveSelectedGender"
        />
      </div>
    </section>
    <main class="grid-main">
      <nav>
        <button
          v-show="adjacentPages.prev != ''"
          v-on:click="getCharacters(adjacentPages.prev)"
        >← Previous</button>
        <button
          v-show="adjacentPages.next != ''"
          v-on:click="getCharacters(adjacentPages.next)"
        >Next →</button>
      </nav>
      <div
        v-if="renderedCharacters.length === 0"
        class="no-results-note"
      >
        <span>No characters match your filters. Try resetting your filters or search the previous or next page of characters.</span>
      </div>
      <CharacterList
        v-else
        :characters="renderedCharacters"
      />
    </main>
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
      characters: [],
      adjacentPages: {
        next: '',
        prev: ''
      },
      visibleStatus: ['Alive', 'Dead', 'unknown'],
      visibleGenders: ['Female', 'Male', 'Genderless', 'unknown'],
      counts: {}
    }
  },
  computed: {
    renderedCharacters: function () {
      return this.characters.filter(character => {
        return this.visibleStatus.includes(character.status) && this.visibleGenders.includes(character.gender)
      })
    },
    noOfMatchingCharacters: function () {
      return this.renderedCharacters.length
    }
  },
  methods: {
    getCharacters: async function (url) {
      const response = await fetch(url)
      const json = await response.json()

      this.characters = json.results
      const { count, next, prev } = json.info
      this.adjacentPages = { next, prev }

      this.counts = {
        total: count,
        page: json.results.length
      }
    },
    receiveSelectedStatus: function (status) {
      console.log('Received selected status', status)
      this.visibleStatus = status
    },
    receiveSelectedGender: function (genders) {
      console.log('Received selected genders', genders)
      this.visibleGenders = genders
    }
  },
  mounted() {
    this.getCharacters('https://rickandmortyapi.com/api/character/')
  }
}
</script>

<style>
/* BASE
----------------------------------------------------- */
:root {
  font-size: 8px;

  --grid-spacing: 2rem;

  --font-size-small: 1.5rem;
  --font-size-regular: 2rem;
  --font-size-large: 3rem;
  --color-primary: rgb(30, 30, 30);
  --color-secondary: rgb(80, 80, 80);
  --color-background: rgb(230, 230, 230);
}
body {
  font-size: var(--font-size-regular);
  font-family: 'Oswald', 'Arial', sans-serif;
  color: var(--color-primary);
  line-height: 1.5;
}

/* LAYOUT
----------------------------------------------------- */
#app {
  height: 100vh;
  padding: var(--grid-spacing);
  display: grid;
  grid-gap: var(--grid-spacing);
  gap: var(--grid-spacing);
  grid-template-columns: 3fr 9fr;
  grid-auto-rows: auto;
}

@media (max-width: 850px) {
  #app {
    grid-template-areas:
      "sidebar sidebar"
      "main main";
  }
}

@media (min-width: 850px) {
  #app {
    grid-template-areas: "sidebar main";
  }
}

.grid-sidebar, .grid-main { padding: var(--grid-spacing); }
.grid-sidebar { grid-area: sidebar; }
.grid-main { grid-area: main; }

.wrapper-sidebar {
  position: sticky;
  top: calc(var(--grid-spacing) * 2);
}

/* TYPOGRAPHY
----------------------------------------------------- */
h1,
h2,
h3,
h4,
h5,
h6 {
  display: block;
  margin-top: var(--grid-spacing);
  margin-bottom: 0;
  font-weight: bold;
}

* > h1,
* > h2,
* > h3,
* > h4,
* > h5,
* > h6 {
    margin-top: 0;
}

h1 { font-size: var(--font-size-large); }
h2, h3, h4, h5, h6 { font-size: var(--font-size-regular); }

p {
  margin-top: var(--grid-spacing);
  margin-bottom: 0;
}

/* BUTTONS
----------------------------------------------------- */
button {
  padding: .6rem 1.2rem;
  margin-right: 1rem;
  background-color: var(--color-background);
  border: 2px solid var(--color-primary);
}
button:focus {
  outline: .1rem dotted black;
}

/* NAV PAGES
----------------------------------------------------- */
nav {
  display: flex;
  justify-content: center;
  position: sticky;
  top: calc(var(--grid-spacing) * 2);
}

/* NO RESULTS NOTE
----------------------------------------------------- */
.no-results-note {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

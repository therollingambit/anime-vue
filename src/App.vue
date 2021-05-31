<template>
  <div class="app">
    <header>
      <h1>The <strong>Anime</strong>DB</h1>
      <form class="search-box" @submit.prevent="handleSearch">
        <input
          type="search"
          class="search-field"
          placeholder="Search for an anime..."
          required
          v-model="search_query"
        />
      </form>
    </header>

    <main>
      <h2 v-if="searchTitle.length > 0">Search for "{{ search_query }}"</h2>
      <div class="cards">
        <Card v-for="anime in animeList" :key="anime.mal_id" :anime="anime" />
      </div>

      <div class="no-results" v-if="animeList.length === 0">
        <h3>Sorry, we have no results...</h3>
      </div>
    </main>
  </div>
</template>

<script>
import Card from "@/components/Card";
import axios from "axios";

export default {
  name: "App",
  components: { Card },
  data() {
    return {
      search_query: "",
      animeList: [],
      searchTitle: "",
    };
  },
  created() {
    this.fetchInit();
  },
  methods: {
    async handleSearch() {
      const res = await axios.get(
        `https://api.jikan.moe/v3/search/anime?q=${this.search_query}`
      );
      const data = await res.data.results;
      this.animeList = data;
      this.searchTitle = this.search_query;
    },
    async fetchInit() {
      const res = await axios.get(
        `https://api.jikan.moe/v3/search/anime?q=demon_slayer`
      );
      const data = await res.data.results;
      this.animeList = data;
      this.search_query = "";
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Fira+Sans&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  font-family: "Fira Sans", sans-serif;
}

a {
  text-decoration: none;
}

header {
  padding-top: 50px;
  padding-bottom: 50px;

  h1 {
    color: #888;
    font-size: 42px;
    font-weight: 400;
    text-align: center;
    text-transform: uppercase;
    margin-bottom: 30px;

    strong {
      color: #313131;
    }

    &:hover {
      color: #313131;
    }
  }

  .search-box {
    display: flex;
    justify-content: center;
    padding: 0 30px;

    .search-field {
      appearance: none;
      background: none;
      border: none;
      outline: none;
      background-color: #f3f3f3;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);

      display: block;
      width: 100%;
      max-width: 600px;
      padding: 15px;
      border-radius: 8px;

      color: #313131;
      font-size: 20px;

      transition: 0.4s;

      &::placeholder {
        color: #aaa;
      }

      &:focus,
      &:valid {
        color: #fff;
        background-color: #313131;
        box-shadow: 0 0 0 rgba(0, 0, 0, 0.15);
      }
    }
  }
}

main {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 30px;

  .cards {
    display: flex;
    flex-wrap: wrap;
    margin: 0 -8px;
    justify-content: space-between;
  }

  h2 {
    padding-bottom: 20px;
  }
}

</style>

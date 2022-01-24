<template>
  <div>
    <search-jokes @search-text="searchText" />
    <joke
      v-for="joke in jokes"
      :key="joke.id"
      :id="joke.id"
      :joke="joke.joke"
    />
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../../components/Joke.vue";
import SearchJokes from "../../components/SearchJokes.vue";
export default {
  components: { Joke, SearchJokes },
  data() {
    return {
      jokes: [],
    };
  },

  created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };

    axios
      .get("https://icanhazdadjoke.com/search", config)
      .then((res) => {
        this.jokes = res.data.results;
      })
      .catch((error) => console.log(error));
  },
  head() {
    return {
      title: "Dad Jokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for corny dad jokes",
        },
      ],
    };
  },

  methods: {
    searchText(text) {
      const config = {
        headers: {
          Accept: "application/json",
        },
      };

      axios
        .get(`https://icanhazdadjoke.com/search?term=${text}`, config)
        .then((res) => {
          this.jokes = res.data.results;
        })
        .catch((error) => console.log(error));
    },
  },
};
</script>

<template>
  <AppHeader @performSearch="getData" />
  <AppMain />
  <AppError v-if="error" />
</template>

<script>
import axios from "axios";
import { store } from "./store";

import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppError from "./components/AppError.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AppMain,
    AppError,
  },
  data() {
    return {
      store,
      error: false,
    };
  },
  methods: {
    getData() {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: "e99307154c6dfb0b4750f6603256716d",
            query: this.store.textToSearch,
            language: "it-IT",
          },
        })
        .then((response) => {
          this.store.movies = response.data.results;
          if (this.error) {
            this.error = !this.error;
          }
        })
        .catch((err) => {
          this.error = true;
        });

      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "e99307154c6dfb0b4750f6603256716d",
            query: this.store.textToSearch,
            language: "it-IT",
          },
        })
        .then((response) => {
          this.store.tv = response.data.results;
          if (this.error) {
            this.error = !this.error;
          }
        })
        .catch((err) => {
          this.error = true;
        });
    },
  },
};
</script>

<style lang="scss" scoped></style>

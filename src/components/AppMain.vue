<template>
  <section>
    <h2>Films</h2>
    <AppCard v-for="movie in store.movies" :info="movie" />
  </section>
  <section>
    <h2>Serie tv</h2>
    <AppCard v-for="tv in store.tv" :info="tv" />
  </section>
</template>

<script>
import { store } from "../store";
import AppCard from "./AppCard.vue";
export default {
  name: "AppMain",
  components: {
    AppCard,
  },
  data() {
    return {
      store,
    };
  },
};
</script>

<style lang="scss" scoped></style>

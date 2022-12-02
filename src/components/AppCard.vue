<template>
  <div>
    <img :src="poster" :alt="title" />
    <h3>{{ title }}</h3>
    <h4>{{ info.original_title || info.original_name }}</h4>
    <div>
      <CountryFlag :country="getFlag(info.original_language)" size="medium" />
    </div>
    <div>
      <font-awesome-icon v-for="n in vote" icon="fa-star fa-solid" />
      <font-awesome-icon v-for="n in 5 - vote" icon="fa-star fa-regular" />
    </div>
  </div>
</template>

<script>
import CountryFlag from "vue-country-flag-next";

export default {
  name: "AppCard",
  props: {
    info: Object,
  },
  components: {
    CountryFlag,
  },
  methods: {
    getFlag(lang) {
      if (lang == "en") {
        return "gb";
      }
      return lang;
    },
  },
  computed: {
    vote() {
      return Math.ceil(this.info.vote_average / 2);
    },
    title() {
      return this.info.title ? this.info.title : this.info.name;
    },
    poster() {
      return this.info.poster_path
        ? `https://image.tmdb.org/t/p/w342${this.info.poster_path}`
        : "https://via.placeholder.com/342x485";
    },
  },
};
</script>

<style lang="scss" scoped></style>

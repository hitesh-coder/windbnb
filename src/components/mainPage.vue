<template>
  <div class="hello">
    <search v-on:locationRecive="getlocation" v-on:noGuestRecive="getGuest" />
    <Content :city="place" :totalGuest="totalGuest" />
    <credits />
  </div>

  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Montserrat:wght@500;600;700&family=Mulish:wght@400;800&display=swap"
    rel="stylesheet"
  />
  <link
    href="https://fonts.googleapis.com/icon?family=Material+Icons"
    rel="stylesheet"
  />
</template>

<script>
import credits from "./Footer/credits.vue";
import search from "./Header/search.vue";
import Content from "./Main/content.vue";

export default {
  name: "MainPage",
  components: { search, Content, credits },
  data() {
    return {
      place: "",
      totalGuest: 0,
    };
  },
  methods: {
    getlocation(value) {
      this.place = value;
    },
    getGuest(value) {
      this.totalGuest = parseInt(value);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>

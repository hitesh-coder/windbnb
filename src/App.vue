<template>
  <main-page />
</template>

<script>
import MainPage from "./components/mainPage.vue";

export default {
  name: "App",
  components: {
    MainPage,
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Montserrat;
}

#app {
  padding: 5% 10%;
}

@media screen and (max-width: 1100px) {
  #app {
    padding: 5vw;
  }
}
</style>

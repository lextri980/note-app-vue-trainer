<template>
  <div id="app">
    <HeaderTab />
    <NoteCard />
  </div>
</template>

<script>
import HeaderTab from "./components/HeaderTab.vue";
import NoteCard from "./components/NoteCard.vue";

export default {
  name: "App",
  components: {
    HeaderTab,
    NoteCard,
  },
};
</script>

<style>
* {
  margin: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100vh;
  width: 100vw;
  overflow-x: hidden;
}
</style>

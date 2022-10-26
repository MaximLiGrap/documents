<template>
  <div id="app">
    <DocumentPage/>
  </div>
</template>

<script>
import DocumentPage from './pages/DocumentPage.vue';

export default {
  name: 'App',
  components: {
    DocumentPage,
  },
};
</script>

<style>
img {
  width: 100%;
}
@font-face {
  font-family: "Fira-Sans";
  src:local("Fira-Sans"),
     url('./fonts/FiraSans-Regular.woff2') format("woff2"),
     url('./fonts/FiraSans-Regular.woff') format("woff");
  font-weight: normal;
  font-style: normal;
}

body {
  font-family: 'Fira-Sans';
}
</style>

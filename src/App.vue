<template>
  <div id="app">
    <Header />
    <Search v-if="!profile" v-on:query="fetchData" /> 
    <Profile v-bind:data="data" v-if="profile" />
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header";
import Search from "./components/Search";
import Profile from "./components/Profile";
import Footer from "./components/Footer";

export default {
  name: 'App',
  data() {
    return {
      profile: false,
      data: ''
    }
  },
  components: {
    Header,
    Search,
    Profile,
    Footer
  },
  methods: {
    fetchData(results) {
      this.data = results;
      this.profile = true;
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Jaldi&family=Roboto&display=swap');

* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Jaldi', sans-serif;
  color: #2c3e50;
}
</style>

<template>
  <header-nav></header-nav>
  <todolist></todolist>
  <footer-nav></footer-nav>
</template>

<script>
import Todolist from "@/components/Todolist.vue";
import HeaderNav from "@/components/Header.vue";
import FooterNav from "@/components/Footer.vue";
export default {
  name: 'App',
  components: {
    FooterNav,
    HeaderNav,
    Todolist,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

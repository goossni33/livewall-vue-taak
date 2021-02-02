<template>
  <div>
    <NavBar/>
    <router-view/>
  </div>
</template>

<style lang="scss">
  .nav {
    background-color: cadetblue;

    .full-width {
      display: flex;
      align-items: center;
    }

    .link {
      margin: 0 12px;
      color: white;
      text-decoration: none;
    }
  }
</style>

<script>
import NavBar from '@/components/NavBar.vue'

export default {
  name: "App",
  components: {
    NavBar
  }
};
</script>
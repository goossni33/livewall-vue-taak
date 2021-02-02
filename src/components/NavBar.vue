<template>
    <div class="nav">
      <div class="full-width">
        <router-link to="/" class="link">Home</router-link>
        <router-link to="/about" class="link">About</router-link>
        <router-link to="/test" class="link">Test</router-link>
      </div>
    </div>
</template>

<script>
export default {
  name: "Navbar"
};
</script>

<style lang="scss">
.nav {
  background-color: cadetblue;
  height: 3rem;
  .title {
    padding: 1rem;
    text-transform: uppercase;
    font-weight: bold;
    color: white;
    display: inline-block;
  }
}
</style>
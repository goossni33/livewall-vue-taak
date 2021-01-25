<template>
  <div>
    <div class="nav">
      <div class="full-width">
        <router-link to="/" class="link">Home</router-link>
        <router-link to="/about" class="link">About</router-link>
      </div>
    </div>
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
<template>
  <div
    id="app"
    class="app"
  >
    <TheNavbar class="app__header" />

    <div class="app__content">
      <router-view />
    </div>
  </div>
</template>

<script>
import TheNavbar from '@/components/the-navbar/TheNavbar'

export default {
  components: {
    TheNavbar
  }
}
</script>

<style lang="scss">
#app {
  background-color: $warmGray-700;
  color: $warmGray-100;
  height: 100vh;

  .app__header {
    margin-bottom: 10px;
  }

  .app__content {
    padding-left: min(50px, 15%);
    padding-right: min(50px, 15%);
  }
}

</style>

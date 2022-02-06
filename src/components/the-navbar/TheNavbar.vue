<template>
  <div class="navbar">
    <div class="navbar__title">
      Keyboard 101
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheNavbar'
}
</script>

<style lang="scss" scoped>
.navbar {
  width: 100%;
  height: 54px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px, rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding-left: min(30px, 10%);
  padding-right: min(30px, 10%);
  font-size: 1.2em;
  background: $amber-500;
  color: $amber-900;
  font-weight: 500;
}
</style>

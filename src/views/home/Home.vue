<template>
  <div class="home">
    <div class="monitor">
      <textarea
        v-model="data.text"
        class="monitor__body"
        autofocus
      >
    </textarea>
    </div>

    <div class="keyboard">
      <HomeKeyboard />
    </div>

    <div class="footer">
      <p>
        Made with ❤ by
        <a
          class="footer__author"
          href="https://jeash.tech"
          target="_blank"
        >
          Ernie Jeash
        </a>
      </p>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

import useBreakpoint from '@/utils/useBreakpoint'

import HomeKeyboard from './components/HomeKeyboard.vue'
import { onMounted, reactive, computed, ref } from 'vue'

export default {
  name: 'Home',

  components: {
    HomeKeyboard
  },

  setup () {
    const { breakpoint } = useBreakpoint()

    const data = reactive({
      text: 'adf'
    })

    return {
      data
    }
  }
}
</script>

<style lang="scss" scoped>
@import './styles/home';
</style>

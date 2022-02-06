<template>
  <div class="home">
    <div class="monitor">
      <textarea
        v-model="text"
        class="monitor__body"
        autofocus
      >
    </textarea>
    </div>

    <div class="keyboard">
      <div
        v-for="(row, rowKey) in keyboardRows"
        :key="rowKey"
        class="keyboard__row"
      >
        <div
          v-for="(rowItem, rowIndex) in row"
          :key="rowIndex"
          class="key"
          :class="{
            [`key--${rowItem.display || rowItem.key}`]: true,
            'key__clicked': isKeyActive({ item: rowItem })
          }"
        >
          <span
            v-if="rowItem.sub"
            class="key__muted"
          >
            {{ rowItem.sub }}
          </span>

          <span>{{ rowItem.display }}</span>
        </div>
      </div>
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

export default {
  name: 'Home',

  data () {
    return {
      activeCodes: new Set(),

      text: ''

    }
  },

  computed: {
    keyboardRows () {
      const keyboard = [
        [
          { display: '`', sub: '~', code: 'Backquote' },
          { display: '1', sub: '!', code: 'Digit1' },
          { display: '2', sub: '@', code: 'Digit2' },
          { display: '3', sub: '#', code: 'Digit3' },
          { display: '4', sub: '$', code: 'Digit4' },
          { display: '5', sub: '%', code: 'Digit5' },
          { display: '6', sub: '^', code: 'Digit6' },
          { display: '7', sub: '&', code: 'Digit7' },
          { display: '8', sub: '*', code: 'Digit8' },
          { display: '9', sub: '(', code: 'Digit9' },
          { display: '0', sub: ')', code: 'Digit0' },
          { display: '-', sub: '_', code: 'Minus' },
          { display: '=', sub: '+', code: 'Equal' },
          { display: 'backspace', code: 'Backspace' }
        ],
        [
          { display: 'tab', code: 'Tab' },
          { display: 'Q', code: 'KeyQ' },
          { display: 'W', code: 'KeyW' },
          { display: 'E', code: 'KeyE' },
          { display: 'R', code: 'KeyR' },
          { display: 'T', code: 'KeyT' },
          { display: 'Y', code: 'KeyY' },
          { display: 'U', code: 'KeyU' },
          { display: 'I', code: 'KeyI' },
          { display: 'O', code: 'KeyO' },
          { display: 'P', code: 'KeyP' },
          { display: '[', sub: '{', code: 'BracketLeft' },
          { display: ']', sub: '}', code: 'BracketRight' },
          { display: '\\', sub: '|', code: 'Backslash' }
        ],
        [
          { display: 'caps', code: 'CapsLock' },
          { display: 'A', code: 'KeyA' },
          { display: 'S', code: 'KeyS' },
          { display: 'D', code: 'KeyD' },
          { display: 'F', code: 'KeyF' },
          { display: 'G', code: 'KeyG' },
          { display: 'H', code: 'KeyH' },
          { display: 'J', code: 'KeyJ' },
          { display: 'K', code: 'KeyK' },
          { display: 'L', code: 'KeyL' },
          { display: ';', sub: ':', code: 'SemiColon' },
          { display: "'", sub: '"', code: 'Quote' },
          { display: 'enter', code: 'Enter' }
        ],
        [
          { display: 'shift', code: 'ShiftLeft' },
          { display: 'Z', code: 'KeyZ' },
          { display: 'X', code: 'KeyX' },
          { display: 'C', code: 'KeyC' },
          { display: 'V', code: 'KeyV' },
          { display: 'B', code: 'KeyB' },
          { display: 'N', code: 'KeyN' },
          { display: 'M', code: 'KeyM' },
          { display: ',', sub: '<', code: 'Comma' },
          { display: '.', sub: '>', code: 'Period' },
          { display: '/', sub: '?', code: 'Slash' },
          { display: 'shift', code: 'ShiftRight' }
        ],
        [
          { display: 'ctrl', code: 'ControlLeft' },
          { display: '⊞', code: 'MetaLeft' },
          { display: 'alt', code: 'AltLeft' },
          { display: 'space', code: 'Space' },
          { display: 'alt', code: 'AltRight' },
          { display: '⊞', code: 'MetaRight' },
          { display: 'ctrl', code: 'ControlRight' }
        ]
      ]

      return keyboard
    }
  },

  mounted () {
    this.bootstrapEvents()
  },

  methods: {
    bootstrapEvents () {
      // Keydown
      const keydownHandler = e => {
        this.activeCodes.add(e.code)

        const prevents = new Set([
          'AltLeft',
          'AltRight',
          'MetaLeft',
          'MetaRight',
          'Tab'
        ])

        if (prevents.has(e.code)) {
          e.preventDefault()
        }

        if (e.altKey) {
          e.preventDefault()
        }
      }

      const keyupHandler = e => {
        this.activeCodes.delete(e.code)
      }

      const clickHandler = e => {
        document.querySelector('.monitor__body').focus()
        this.activeCodes.clear()
      }

      const blurHandler = e => {
        this.activeCodes.clear()
      }

      const events = [
        { type: document, event: 'keydown', handler: keydownHandler },
        { type: document, event: 'keypress', handler: keydownHandler },
        { type: document, event: 'keyup', handler: keyupHandler },
        { type: document, event: 'click', handler: clickHandler },
        { type: window, event: 'blur', handler: blurHandler }
      ]

      events.forEach(e => {
        document.addEventListener(e.event, e.handler)
        window.addEventListener(e.event, e.handler)
      })
    },

    isKeyActive ({ item }) {
      const activeCodes = this.activeCodes

      if (!activeCodes.size) {
        return false
      }

      return activeCodes.has(item.code)
    }
  }
}
</script>

<style lang="scss" scoped>
@import './styles/home';
</style>

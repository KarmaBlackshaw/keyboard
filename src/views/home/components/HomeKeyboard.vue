<template>
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
          [`key--${rowItem.code}`]: true,
          'key__clicked': isKeyActive({ item: rowItem })
        }"
      >
        <span
          v-if="rowItem.sub"
          class="key__muted"
        >
          {{ rowItem.sub.display }}
        </span>

        <span>{{ rowItem.display }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, ref, onMounted, reactive } from 'vue'
import useBreakpoint from '@/utils/useBreakpoint'

export default {
  name: 'HomeKeyboard',

  setup () {
    const { breakpoint } = useBreakpoint()

    const state = reactive({
      text: '',
      isShift: false,
      isCapsLock: false
    })

    const keyboardRows = computed(() => {
      const keyboard = [
        [
          {
            display: '`',
            code: 'Backquote',
            is_hidden: breakpoint.value.smAndBelow,
            sub: {
              display: '~'
            }
          },
          {
            display: '1',
            code: 'Digit1',
            sub: {
              display: '!'
            }
          },
          {
            display: '2',
            code: 'Digit2',
            sub: {
              display: '@'
            }
          },
          {
            display: '3',
            code: 'Digit3',
            sub: {
              display: '#'
            }
          },
          {
            display: '4',
            code: 'Digit4',
            sub: {
              display: '$'
            }
          },
          {
            display: '5',
            code: 'Digit5',
            sub: {
              display: '%'
            }
          },
          {
            display: '6',
            code: 'Digit6',
            sub: {
              display: '^'
            }
          },
          {
            display: '7',
            code: 'Digit7',
            sub: {
              display: '&'
            }
          },
          {
            display: '8',
            code: 'Digit8',
            sub: {
              display: '*'
            }
          },
          {
            display: '9',
            code: 'Digit9',
            sub: {
              display: '('
            }
          },
          {
            display: '0',
            code: 'Digit0',
            sub: {
              display: ')'
            }
          },
          {
            display: '-',
            code: 'Minus',
            is_hidden: breakpoint.value.smAndBelow,
            sub: {
              display: '_'
            }
          },
          {
            display: '=',
            code: 'Equal',
            is_hidden: breakpoint.value.smAndBelow,
            sub: {
              display: '+'
            }
          },
          {
            display: breakpoint.value.smAndBelow ? '⌫' : 'backspace',
            code: 'Backspace'
          }
        ],
        [
          {
            display: breakpoint.value.smAndBelow ? '↹' : 'tab',
            code: 'Tab'
          },
          {
            display: 'Q',
            code: 'KeyQ'
          },
          {
            display: 'W',
            code: 'KeyW'
          },
          {
            display: 'E',
            code: 'KeyE'
          },
          {
            display: 'R',
            code: 'KeyR'
          },
          {
            display: 'T',
            code: 'KeyT'
          },
          {
            display: 'Y',
            code: 'KeyY'
          },
          {
            display: 'U',
            code: 'KeyU'
          },
          {
            display: 'I',
            code: 'KeyI'
          },
          {
            display: 'O',
            code: 'KeyO'
          },
          {
            display: 'P',
            code: 'KeyP'
          },
          {
            display: '[',
            code: 'BracketLeft',
            is_hidden: breakpoint.value.smAndBelow,
            sub: {
              display: '{'
            }
          },
          {
            display: ']',
            code: 'BracketRight',
            is_hidden: breakpoint.value.smAndBelow,
            sub: {
              display: '}'
            }
          },
          {
            display: '\\',
            code: 'Backslash',
            is_hidden: breakpoint.value.smAndBelow,
            sub: {
              display: '|'
            }
          }
        ],
        [
          {
            display: breakpoint.value.smAndBelow ? '⇪' : 'caps',
            code: 'CapsLock'
          },
          {
            display: 'A',
            code: 'KeyA'
          },
          {
            display: 'S',
            code: 'KeyS'
          },
          {
            display: 'D',
            code: 'KeyD'
          },
          {
            display: 'F',
            code: 'KeyF'
          },
          {
            display: 'G',
            code: 'KeyG'
          },
          {
            display: 'H',
            code: 'KeyH'
          },
          {
            display: 'J',
            code: 'KeyJ'
          },
          {
            display: 'K',
            code: 'KeyK'
          },
          {
            display: 'L',
            code: 'KeyL'
          },
          {
            display: ';',
            sub: ':',
            code: 'SemiColon',
            is_hidden: breakpoint.value.smAndBelow
          },
          {
            display: "'",
            sub: '"',
            code: 'Quote',
            is_hidden: breakpoint.value.smAndBelow
          },
          {
            display: breakpoint.value.smAndBelow ? '↵' : 'enter',
            code: 'Enter'
          }
        ],
        [
          {
            display: breakpoint.value.smAndBelow ? '⇧' : 'shift',
            code: 'ShiftLeft'
          },
          {
            display: 'Z',
            code: 'KeyZ'
          },
          {
            display: 'X',
            code: 'KeyX'
          },
          {
            display: 'C',
            code: 'KeyC'
          },
          {
            display: 'V',
            code: 'KeyV'
          },
          {
            display: 'B',
            code: 'KeyB'
          },
          {
            display: 'N',
            code: 'KeyN'
          },
          {
            display: 'M',
            code: 'KeyM'
          },
          {
            display: ',',
            code: 'Comma',
            sub: {
              display: '<'
            },
            is_hidden: breakpoint.value.smAndBelow
          },
          {
            display: '.',
            code: 'Period',
            sub: {
              display: '>'
            },
            is_hidden: breakpoint.value.smAndBelow
          },
          {
            display: '/',
            code: 'Slash',
            sub: {
              display: '?'
            },
            is_hidden: breakpoint.value.smAndBelow
          },
          {
            display: breakpoint.value.smAndBelow ? '⇧' : 'shift',
            code: 'ShiftRight'
          }
        ],
        [
          {
            display: breakpoint.value.smAndBelow ? '⎵' : 'space',
            code: 'Space'
          }
        ]
      ]

      keyboard.forEach((row, i) => {
        keyboard[i] = row.filter(x => !x.is_hidden)
      })

      return keyboard
    })

    const activeCodes = ref(new Set())

    function isKeyActive ({ item }) {
      if (!activeCodes.value.size) {
        return false
      }

      return activeCodes.value.has(item.code)
    }

    const keyboardEvents = {
      keydownHandler: e => {
        activeCodes.value.add(e.code)

        const prevents = new Set([
          'AltLeft',
          'AltRight',
          'MetaLeft',
          'MetaRight',
          'ControlLeft',
          'ControlRight',
          'Tab'
        ])

        if (prevents.has(e.code)) {
          e.preventDefault()
        }

        if (e.altKey) {
          e.preventDefault()
        }

        const invalidCodes = new Set([
          'Control',
          'Tab',
          'CapsLock',
          'Shift'
        ])

        if (!invalidCodes.has(e.code)) {
          state.text += e.key
        }
      },

      keyupHandler: e => {
        activeCodes.value.delete(e.code)

        if (e.getModifierState('CapsLock')) {
          activeCodes.value.add('CapsLock')
        }
      },

      blurHandler: e => {
        activeCodes.value.clear()
      }
    }

    function bootstrapEvents () {
      const events = [
        { type: document, event: 'keydown', handler: keyboardEvents.keydownHandler },
        { type: document, event: 'keyup', handler: keyboardEvents.keyupHandler },
        { type: window, event: 'blur', handler: keyboardEvents.blurHandler }
      ]

      events.forEach(e => {
        document.addEventListener(e.event, e.handler)
      })
    }

    onMounted(() => {
      bootstrapEvents()
    })

    return {
      keyboardRows,
      isKeyActive,
      keyboardEvents,
      activeCodes
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../styles/home-keyboard';
</style>

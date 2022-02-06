<template>
  <div class="home">
    <textarea
      v-model="text"
      class="monitor"
      autofocus
    >
    </textarea>

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
            'key__clicked': isKeyActive({item: rowItem})
          }"
        >
          <span
            v-if="rowItem.superset"
            class="key__muted"
          >
            {{ rowItem.superset }}
          </span>

          <span>{{ rowItem.display || rowItem.key }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',

  data () {
    return {
      activeKeys: new Set(),

      text: ''

    }
  },

  computed: {
    keyboardRows () {
      return [
        [
          { key: '`', superset: '~' },
          { key: '1', superset: '!' },
          { key: '2', superset: '@' },
          { key: '3', superset: '#' },
          { key: '4', superset: '$' },
          { key: '5', superset: '%' },
          { key: '6', superset: '^' },
          { key: '7', superset: '&' },
          { key: '8', superset: '*' },
          { key: '9', superset: '(' },
          { key: '0', superset: ')' },
          { key: '-', superset: '_' },
          { key: '=', superset: '+' },
          { key: 'backspace' }
        ],
        [
          { key: 'tab' },
          { key: 'Q' },
          { key: 'W' },
          { key: 'E' },
          { key: 'R' },
          { key: 'T' },
          { key: 'Y' },
          { key: 'U' },
          { key: 'I' },
          { key: 'O' },
          { key: 'P' },
          { key: '[', superset: '{' },
          { key: ']', superset: '}' },
          { key: '\\', superset: '|' }
        ],
        [
          { key: 'caps' },
          { key: 'A' },
          { key: 'S' },
          { key: 'D' },
          { key: 'F' },
          { key: 'G' },
          { key: 'H' },
          { key: 'J' },
          { key: 'K' },
          { key: 'L' },
          { key: ';', superset: ':' },
          { key: "'", superset: '"' },
          { key: 'enter' }
        ],
        [
          { key: 'shift' },
          { key: 'Z' },
          { key: 'X' },
          { key: 'C' },
          { key: 'V' },
          { key: 'B' },
          { key: 'N' },
          { key: 'M' },
          { key: ',', superset: '<' },
          { key: '.', superset: '>' },
          { key: '/', superset: '?' },
          { key: 'shift' }
        ],
        [
          { display: 'ctrl', key: 'control' },
          { display: '⊞', key: 'meta' },
          { key: 'alt' },
          { display: 'space', key: ' ' },
          { key: 'alt' },
          { display: '⊞', key: 'meta' },
          { display: 'ctrl', key: 'control' }
        ]
      ]
    }
  },

  mounted () {
    this.bootstrapEvents()
  },

  methods: {
    bootstrapEvents () {
      // Keydown
      const keydownHandler = e => {
        this.activeKeys.add(e.key.toLowerCase())
      }

      const keyupHandler = e => {
        this.activeKeys.delete(e.key.toLowerCase())
      }

      const clickHandler = e => {
        document.querySelector('.monitor').focus()
      }

      const blurHandler = e => {
        this.activeKeys.clear()
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
      })
    },

    isKeyActive ({ item }) {
      const activeKeys = this.activeKeys
      const key = item.key.toLowerCase()

      if (activeKeys.has(key)) {
        return true
      }

      if (item.superset) {
        const superset = item.superset.toLowerCase()

        return activeKeys.has(superset)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  height: 100%;
  width: 100%;
}

.monitor {
  height: 300px;
  width: 100%;
  border: 1px solid $warmGray-500;
  margin-bottom: 20px;
  overflow-y: auto;
  padding: 10px;
  font-size: 0.9rem;
  color: $warmGray-400;
  background: transparent;
  resize: none;
  border-radius: 5px;
  user-select: none;

  &:focus {
    outline: none;
  }
}

.keyboard {
  .keyboard__row {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .key {
    height: 45px;
    min-width: 45px;
    font-family: monospace;
    font-size: 0.9rem;
    display: flex;
    justify-content: space-around;
    align-items: center;
    border: 1px solid $warmGray-500;
    color: $warmGray-500;
    border-radius: 5px;
    flex-direction: column;
    padding: 5px;
    user-select: none;
    margin: 3px;
    line-height: 100%;
    text-transform: uppercase;

    .key__muted {
      color: $warmGray-600;
      text-align: left;
      margin: 0;
      padding: 0;
      line-height: 100%;
      font-size: 0.8rem;
      width: 100%;
      flex-grow: 1;
      flex:0 0 auto;
    }

    &.key__clicked {
      border: 1px solid $amber-400;
      color: white;
      background-color: $amber-400;
    }

    &.key--tab {
      width: 70px;
    }

    &.key--caps {
      width: 70px;
    }

    &.key--shift {
      width: 90px;
    }

    &.key--enter {
      width: 100px;
    }

    &.key--space {
      width: 300px;
    }
  }
}
</style>

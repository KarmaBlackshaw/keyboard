<template>
  <div class="home">
    <div class="keyboard">
      {{ activeKeys }}
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
      activeKeys: new Set()
    }
  },

  computed: {
    keyboardRows () {
      return [
        [
          { key: '`', superset: '~' },
          { key: '1' },
          { key: '2' },
          { key: '3' },
          { key: '4' },
          { key: '5' },
          { key: '6' },
          { key: '7' },
          { key: '8' },
          { key: '9' },
          { key: '0' },
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
    document.addEventListener('keydown', e => {
      this.activeKeys.add(e.key.toLowerCase())
      e.preventDefault()
    })

    document.addEventListener('keyup', e => {
      this.activeKeys.delete(e.key.toLowerCase())
      e.preventDefault()
    })

    window.addEventListener('blur', () => {
      this.activeKeys.clear()
    })
  },

  methods: {
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
  display: flex;
  justify-content: center;
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
    font-size: 1.1rem;
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

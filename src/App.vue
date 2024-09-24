<template>
  <router-view />
</template>

<script lang="ts">
declare global {
  interface String {
    stripMargin(marginChar?: string): string;
    isEmpty(): boolean;
    isNotEmpty(): boolean;
  }
  interface Array<T> {
    remove(toRemove: T) : boolean
  }
}

export default {
  name: 'App',
  setup () {
    // eslint-disable-next-line no-extend-native
    Array.prototype.remove = function <T> (toRemove: T) : boolean {
      const indexOf = this.indexOf(toRemove)
      if (indexOf > -1) {
        this.slice(indexOf, 1)
        return true
      }
      return false
    }
    // eslint-disable-next-line no-extend-native
    String.prototype.stripMargin = function (marginChar = '|') {
      return this.split('\n')
        .map(line => {
          const pos = line.indexOf(marginChar)
          return pos >= 0 ? line.slice(pos + 1) : line
        })
        .join('\n')
    }
    // eslint-disable-next-line no-extend-native
    String.prototype.isEmpty = function () {
      return this.length === 0
    }
    // eslint-disable-next-line no-extend-native
    String.prototype.isNotEmpty = function () {
      return this.length > 0
    }
    return {}
  }
}
</script>

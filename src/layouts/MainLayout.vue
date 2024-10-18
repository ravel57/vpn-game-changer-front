<template lang="pug">
q-layout(view='lHh Lpr lFf' class="main")
  q-page-container
    router-view
</template>

<script lang="ts">

export default {
  name: 'MainLayout',

  components: {
  },

  data: () => ({
    leftDrawerOpen: false
  }),

  methods: {
  }
}
</script>

<style scoped>
.main {
  margin: 16px;
}
</style>

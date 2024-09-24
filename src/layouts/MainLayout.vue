<template lang="pug">
q-layout(view='lHh Lpr lFf')
  q-header(elevated)
    q-toolbar
      q-btn(flat dense round icon='menu' aria-label='Menu' @click='toggleLeftDrawer')
        q-toolbar-title
          | Vpn game changer
  q-drawer(v-model='leftDrawerOpen' show-if-above bordered)
    q-list
      q-item-label(header)
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
    toggleLeftDrawer () {
      this.leftDrawerOpen = !this.leftDrawerOpen
    }
  }
}
</script>

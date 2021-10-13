<template>
  <q-layout view="hHh lpR fFf">

    <q-header class="bg-green-3 text-white">
      <q-toolbar>


        <q-toolbar-title class = "text-weight-bolder on-right" style="font-size: 25pt">
          Hourly
        </q-toolbar-title>
      </q-toolbar>

    </q-header>

    <q-drawer v-model="leftDrawerOpen" side="left" overlay elevated>
      <!-- drawer content -->
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const leftDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
}
</script>

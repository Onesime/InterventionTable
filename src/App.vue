<template>
  <div id="app">

    <router-view/>
  </div>
</template>

<script>

import InterventionTable from './components/InterventionTable'

export default {
  name: 'App',
  components: {
      InterventionTable: InterventionTable
  }
}
</script>

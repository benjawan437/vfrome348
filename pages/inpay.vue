<template>
  <div id="app">
    <v-row justify="center" align="center">
      <v-col cols="12" lg="8" md="6">
        <pay></pay>
        <show></show>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import pay from '@/pages/pay'
export default {
  components: {
    pay,
  },
}
</script>

<style>
#app {
  font-family: 'Prompt', sans-serif;
}
</style>

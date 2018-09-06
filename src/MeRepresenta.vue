<template>
  <div id="app">
    <MeRerpesentaCandidatesExplorer/>
  </div>
</template>

<script>
import MeRerpesentaCandidatesExplorer from './components/MeRerpesentaCandidatesExplorer'

export default {
  name: 'MeRepresenta',
  components: {
    MeRerpesentaCandidatesExplorer
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

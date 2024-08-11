<template>
  <GeneradorNumeros msg="Generador de Números de Lotería"/>
</template>

<script>
import GeneradorNumeros from './components/GeneradorNumeros.vue'

export default {
  name: 'App',
  components: {
    GeneradorNumeros
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

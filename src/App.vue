<template>
  <div id="app">
    <Botao/>
    <Calendario/>
  </div>
</template>

<script>
import Calendario from '@/components/Calendario'
import Botao from '@/components/Botao'
import FormModal from '@/components/FormModal'

export default {
  name: 'App',
  components: {
    Calendario,
    Botao,
    'form-modal': FormModal
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

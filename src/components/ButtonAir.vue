<template>
  <button class="btn button-air" :class="buttonAirStyle" >
    <i v-if="this.estilo == 'icone'" :class="this.iconclass"></i>
    <i v-if="this.estilo == 'excel'" :class="this.iconclass"></i>
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    mode: null,
    estilo: {
      required: false,
      default: 'principal',
      type: String
    },
    iconclass: {
      required: false,
      default: 'far fa-trash-alt',
      type: String
    }
  },
  computed: {
    buttonAirStyle () {
      var retorno = ''
      if (this.estilo === 'principal') retorno = 'principal'
      if (this.estilo === 'secundario') retorno = 'secundario'
      if (this.estilo === 'icone') retorno = 'icone'
      if (this.estilo === 'excel') retorno = 'excel'

      if (this.mode === 'chuby') {
        retorno = retorno + ' chuby-btn'
      }
      return retorno
    }
  }
}
</script>

<style lang="scss" scoped>
.button-air {
  // margin-right: 5px;
  // padding-left: 15px;
  padding-right: 15px;
  padding-top: 10px;
  padding-bottom: 10px;
  // margin-bottom: 15px;
  cursor: pointer;
  color: #fff;
  border-radius: 60px;
  min-width: 150px;
  height: 40px;
  -webkit-appearance: button;
  font-family: Poppins;
  box-sizing: border-box;
  -webkit-text-size-adjust: 100%;
  -webkit-tap-highlight-color: transparent;
  font-family: "Poppins", sans-serif;
  font-size: 13px;
  font-weight: 500;
}

.chuby-btn{
  padding-top: 15px;
  padding-bottom: 35px;
}

.principal {
  background-color: #0081ff;
  border-color: #0081ff;
  box-shadow: 0 5px 10px 2px rgba(88, 103, 221, 0.19) !important;

  &:hover {
    background-color: #006fd6;
    border-color: #006fd6;
    -webkit-box-shadow: 0 5px 10px 2px rgba(88, 103, 221, 0.36) !important;
    -moz-box-shadow: 0 5px 10px 2px rgba(88, 103, 221, 0.36) !important;
    box-shadow: 0 5px 10px 2px rgba(88, 103, 221, 0.36) !important;
  }
}
.secundario {
  background-color: white;
  border: 1px solid #666674;
  color: #666674;
  box-shadow: 0 5px 10px 2px rgba(0, 0, 0, 0.19) !important;
  &:hover {
    background-color: #006fd6;
    border-color: #006fd6;
    color: white;
    -webkit-box-shadow: 0 5px 10px 2px rgba(88, 103, 221, 0.36) !important;
    -moz-box-shadow: 0 5px 10px 2px rgba(88, 103, 221, 0.36) !important;
    box-shadow: 0 5px 10px 2px rgba(0, 0, 0, 0.36) !important;
  }
}

.icone {
  background-color: #f4516c;
  border: 1px solid #f4516c;
  color: white;
  box-shadow: 0 5px 10px 2px rgba(244, 81, 108, 0.19) !important;
  &:hover {
    background-color: #e43e5a;
    border-color: #e43e5a;
    color: white;
    -webkit-box-shadow: 0 5px 10px 2px rgba(244, 81, 108, 0.36) !important;
    -moz-box-shadow: 0 5px 10px 2px rgba(244, 81, 108, 0.36) !important;
    box-shadow: 0 5px 10px 2px rgba(244, 81, 108, 0.36) !important;
  }
}

.excel {
  background-color: #20c99a;
  border: 1px solid #20c99a;
  color: white;
  box-shadow: 0 5px 10px 2px rgba(30,185,141, 0.19) !important;
  &:hover {
    background-color: #1eb98d;
    border-color: #1eb98d;
    color: white;
    -webkit-box-shadow: 0 5px 10px 2px rgba(24,145,111, 0.36) !important;
    -moz-box-shadow: 0 5px 10px 2px rgba(24,145,111, 0.36) !important;
    box-shadow: 0 5px 10px 2px rgba(24,145,111, 0.36) !important;
  }
}

i {
  margin-right: 0.5em;
}
</style>

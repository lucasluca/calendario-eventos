<template>
  <div class="category-modal">
    <div class="header">
      <h3 v-if="!title">Insira um Evento</h3>
      <h3 v-if="title">Editar Evento</h3>
      <i @click="closeModal" class="fas fa-times"></i>
    </div>
    <div class="body">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import SelectInput from '@/components/SelectInput'
import InputText from '@/components/InputText'
import ButtonAir from '@/components/ButtonAir'

export default {
  components: {
    'select-input': SelectInput,
    'input-text': InputText,
    'button-air': ButtonAir
  },
  props: {
    title: {
      default: false,
      required: false,
      type: Boolean
    }
  },
  methods: {
    closeModal () {
      this.$emit('closeModal')
    }
  }
}
</script>

<style lang="scss" scoped>
.category-modal {
  // height: 639px;
  width: 443px;
  background-color: white;
  -webkit-box-shadow: 0px 0px 34px -10px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 0px 0px 34px -10px rgba(0, 0, 0, 0.75);
  box-shadow: 0px 0px 34px -10px rgba(0, 0, 0, 0.75);

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    border-bottom: 2px solid rgba(102, 102, 116, 0.2);
    margin-bottom: 10px;

    h3 {
      margin: 0;
      font-size: 16px;
      font-weight: 600;
    }

    i {
      cursor: pointer;
    }
  }

  .body {
    padding: 10px 20px;
    border-bottom: 1px solid rgba(102, 102, 116, 0.4);
    margin-bottom: 10px;

    .select-input {
      margin-bottom: 10px;
    }

    .input-text {
      margin-bottom: 10px;
    }
  }

  .footer {
    display: flex;
    padding: 10px 20px;
    justify-content: flex-end;
    align-items: center;
    margin: auto 0;
    margin-bottom: 15px;
    .button-air {
      margin-right: 10px;
    }
  }
}
</style>

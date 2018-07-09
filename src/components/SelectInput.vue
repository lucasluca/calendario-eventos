<template>
  <div class="select-input" :style="style">
    <label v-if="label" :for="this.nameId">{{ label }}</label>
    <select @change="emitSelection" v-model="value" class="select-tag" :name="this.nameId" id="">
      <option v-if="displayDefaultOption" disabled :selected="displayDefaultOption" value="">Escolha uma opcao</option>
      <slot></slot>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    nameId: {
      required: true,
      type: String
    },
    widths: {
      required: false,
      default: '100%',
      type: String
    },
    label: {
      required: false,
      default: '',
      type: String
    },
    displayDefaultOption: {
      required: false,
      default: true
    },
    getBackDefault: {
      required: false
    },
    actualOption: {
      required: false
    }
  },

  watch: {
    getBackDefault () {
      this.value = '';
    },
    actualOption () {
      this.value = this.actualOption;
    }
  },

  data () {
    return {
      value: ''
    }
  },

  methods: {
    emitSelection () {
      this.$emit('onChange', this.value)
    }
  },

  computed: {
    style () {
      return `width: ${this.widths}`
    }
  }
}
</script>

<style lang="scss" scoped>
.select-input {
  width: 100%;
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  font-family: "Poppins", sans-serif;
  font-weight: 500;
  font-size: 14px;
  color: #666674;

  .select-tag {
    font-family: "Roboto", sans-serif;
    font-weight: 400;
    font-size: 14px;
    color: #666674;
    width: 100%;
    border: 1px solid #ebedf2;
    // margin-bottom: 0.3em;
    background-color: white;
    height: 37px;
  }
}
</style>

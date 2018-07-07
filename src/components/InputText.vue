<template>
  <div class="text" :style="style" :class='myMode'>
    <label :for="this.nameId">
      <slot></slot>
    </label>
    <input type="text" :placeholder="this.placeholder" :name="this.nameId">
    <small v-if="this.instruction">{{ instruction }}</small>
  </div>
</template>

<script>
export default {

  props: {
    nameId: {
      required: false,
      type: String
    },
    placeholder: {
      required: false,
      type: String,
      default: 'Insert a value in the component'
    },
    instruction: {
      required: false,
      type: String,
      default: ''
    },
    widths: {
      required: false,
      default: '100%',
      type: String
    },
    mode: {
      required: false,
      type: String,
      default: 'none'
    }
  },
  computed: {
    style () {
      return `width: ${this.widths}`
    },
    myMode () {
      if (this.mode === 'charm') {
        return 'charm-input'
      } else {
        return ''
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.text {
  width: 100%;
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  label {
    font-family: "Poppins", sans-serif;
    font-weight: 500;
    font-size: 14px;
    color: #666674;
  }
  input {
    font-family: "Roboto", sans-serif;
    font-weight: 400;
    font-size: 14px;
    color: #666674;
    padding: 0.4em;
    height: 37px;
    width: 100%;
    border: 1px solid #ebedf2;
    // margin-bottom: 0.3em;
  }
  small {
    font-family: "Poppins", sans-serif;
    font-weight: 400;
    font-size: 12px;
    color: #666674;
  }
}

.charm-input {
  label {
    color: white;
  }

  input {
    border: 0px;
    background: transparent;
    color: rgb(0, 0, 0);
  }

  input:focus {
    outline: none;
  }

  input:focus::placeholder {
    outline: none;
    color: rgb(101, 178, 255);
  }

  label {
    display: none;
  }
}
</style>

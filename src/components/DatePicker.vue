<!-- https://github.com/ankurk91/vue-flatpickr-component
Vue.js component for Flatpickr datetime picker
# npm
#npm install vue-flatpickr-component --save

# Yarn
yarn add vue-flatpickr-component -->
<template>
  <div class="datetimeinput" :style="style">
    <label class="label" for="">
      <slot></slot>
    </label>
    <div class="datewrapper">
      <flat-pickr :placeholder="this.placeholder" class="datepicker" :config="config" v-model="date"></flat-pickr>
      <div class="input-group-btn">
        <button class="" type="button" title="Toggle" data-toggle>
          <i v-if="clock" class="far fa-clock"></i>
          <i v-else class="far fa-calendar-check"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import flatPickr from 'vue-flatpickr-component'
import 'flatpickr/dist/flatpickr.css'
import { Portuguese } from 'flatpickr/dist/l10n/pt'

export default {
  data: () => {
    return {
      date: null,
      config: {
        wrap: true,
        enableTime: false,
        noCalendar: false,
        time_24hr: false,
        locale: Portuguese // locale for this instance only
      },
      clock: false
    }
  },
  components: {
    flatPickr
  },
  props: {
    type: {
      type: String,
      default: 'date',
      required: false
    },
    placeholder: {
      type: String,
      default: 'Selecione a data',
      required: false
    },
    widths: {
      required: false,
      default: '100%',
      type: String
    }
  },
  computed: {
    style () {
      return `width: ${this.widths}`
    }
  },
  created () {
    switch (this.type.toLowerCase()) {
      case 'date':
        this.config.enableTime = false
        return
      case 'time':
        this.config.enableTime = true
        this.config.noCalendar = true
        this.clock = true
        return
      case 'datetime':
        this.config.enableTime = true
        return
      default:
        this.config.enableTime = false
    }
  }
}
</script>

<style lang="scss" scoped>
.datetimeinput {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  .label {
    font-family: "Poppins", sans-serif;
    font-size: 14px;
    font-weight: 500;
    color: #666674;
  }
}

.datewrapper {
  display: flex;
  background-color: white;
  border: 1px solid #ebedf2;
  border-radius: 5px;
  height: 37px;

  .datepicker {
    font-family: "Poppins", sans-serif;
    font-size: 14px;
    width: 100%;
    font-weight: 400;
    color: #666674;
    border: none;
    padding: 0.9em;
  }
  button {
    height: 100%;
    background-color: #f4f5f8;
    border: none;
    border-left: 1px solid #ebedf2;
    width: 45px;
    margin: 0;

    i {
      color: #9699a2;
      font-size: 18px;
      margin: 0;
    }
  }
}
</style>

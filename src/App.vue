<template>
  <div id="app">
    <button-air>Cadastrar Evento</button-air>
    <full-calendar :config="config" :events="eventsData" @event-selected="editEvent"/>
    <form-modal title="Insira um novo evento">
      <form @submit.prevent action="">
        <input-text v-model="evento.title" class="input-text" nameId="teste" placeholder="Testando componente" instruction="">Nome</input-text>
        <input-text v-model="evento.local" class="input-text" nameId="teste" placeholder="Testando componente" instruction="">Local</input-text>
        <div>
          <flat-pickr placeholder="Data Inicial"  :config="configCalendar" v-model="evento.start"></flat-pickr>
        </div>
        <br>
        <div>
          <flat-pickr placeholder="Data Final" class="datepicker" :config="configCalendar" v-model="evento.end"></flat-pickr>
        </div>
        <br>
        <select-input @onChange='tipoEvento' class="select-input" label="Tipo de Evento" nameId="selec-loja">
          <option selected disabled>Nenhum tipo</option>
          <option value="reuniao">Reunião</option>
          <option value="festa">Evento Festivo</option>
          <option value="consulta">Consulta Médica</option>
        </select-input>
        <div class="footer">
          <button-air @click.native="clearData" class="button-air" estilo="secundario">Cancelar</button-air>
          <button-air @click.native="addEvent">Confirmar</button-air>
          <button-air @click.native="editOk">Editar</button-air>
        </div>
      </form>
    </form-modal>
  </div>
</template>

<script>
import Calendario from '@/components/Calendario'
import Botao from '@/components/Botao'
import FormModal from '@/components/FormModal'
import ButtonAir from '@/components/ButtonAir'
import InputText from '@/components/InputText'
import SelectInput from '@/components/SelectInput'
import DatePicker from '@/components/DatePicker'
import moment from 'moment'
import 'fullcalendar/dist/locale/pt-br'
import flatPickr from 'vue-flatpickr-component'
import 'flatpickr/dist/flatpickr.css'
import { Portuguese } from 'flatpickr/dist/l10n/pt'

export default {
  name: 'App',
  components: {
    Calendario,
    Botao,
    'form-modal': FormModal,
    'button-air': ButtonAir,
    'input-text': InputText,
    'select-input': SelectInput,
    'date-picker': DatePicker,
    flatPickr
  },
  data () {
    return {
      updateIndex: '',
      evento: {
        id: 5,
        title: '',
        local: '',
        start: '',
        end: '',
        color: '',
      },
			eventsData: [
				{
            id: 1,
            title  : 'event1',
            start  : '2018-07-01',
            color: 'red'
        },
        {
            id: 2,
            title  : 'event2',
            start  : '2018-07-05',
            end    : '2018-07-07',
            color: 'green'
        },
        {
            id: 3,
            title  : 'event3',
            start  : '2018-07-05T12:30:00',
            allDay : false,
            color: 'black'
        },
        {
            id: 4,
            title  : 'Eduarda',
            start  : '2018-07-05T12:30:00',
            end    : '2018-07-07',
            allDay : false,
            color: 'purple'
        },
        {
            id: 5,
            title  : 'Lucas',
            start  : '2018-07-05T12:30:00',
            end    : '2018-07-07',
            allDay : false,
        },
			],
			config: {
        defaultView: 'month',
				locale: 'pt-br',
				editable: false,
				eventRender: function(event, element) {
        	// console.log(event)
    		}
      },
      configCalendar: {
        wrap: true,
        enableTime: true,
        noCalendar: false,
        time_24hr: false,
        locale: Portuguese // locale for this instance only
      }
    }
  },
  methods: {
    recebidoData (data) {
      console.log(data);
    },
    clearData () {
      this.evento.title = '';
      this.evento.local = '';
      this.evento.start = '';
      this.evento.end = '';
    },
    addEvent() {
      this.increment();
      this.eventsData.push(Object.assign({}, this.evento));
      this.clearData();
    },
    editEvent(eventoRec) {
      console.log(eventoRec.id);
      this.evento.title = eventoRec.title;
      this.evento.local = eventoRec.local;
      this.evento.start = eventoRec.start._i;
      this.evento.end = eventoRec.end._i;
      this.updateIndex = this.eventsData.map(eventData => eventData.id).indexOf(eventoRec.id);
    },
    editOk () {
      this.eventsData.splice(this.updateIndex, 1);
      this.addEvent();
    },
    increment () {
      this.evento.id ++;
    },
    tipoEvento (tipo) {
      console.log(tipo);
      if(tipo == )
    }
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

<template>
  <div id="app">
    <button-air @click.native="showModal">Cadastrar Evento</button-air>
    <!-- Lib para renderização do Calendario -->
    <full-calendar :config="config" :events="eventsData" @event-selected="editEvent"/>
    <div class="modal-1" :class="classModal">
      <form-modal :title="isEdit" @closeModal="showModal">
        <form @submit.prevent action="">
          <input-text v-model="evento.title" class="input-text" nameId="teste" placeholder="Insira o nome do Evento" instruction="">Nome</input-text>
          <input-text v-model="evento.local" class="input-text" nameId="teste" placeholder="Insira o Local do Evento" instruction="">Local</input-text>
          <date-picker>
            <template slot="label">
              Data Inicial
            </template>
            <template slot="picker">
              <flat-pickr class="datepicker" placeholder="Data Inicial"  :config="configCalendar" v-model="evento.start"></flat-pickr>
            </template>
          </date-picker>
          <br>
          <date-picker>
            <template slot="label">
              Data Final
            </template>
            <template slot="picker">
              <flat-pickr placeholder="Data Final" class="datepicker" :config="configCalendar" v-model="evento.end"></flat-pickr>
            </template>

          </date-picker>
          <br>
          <select-input :getBackDefault='defaultSelect' :actualOption="actualOption" @onChange='tipoEvento' class="select-input" label="Tipo de Evento" nameId="selec-loja">
            <option value="reuniao">Reunião</option>
            <option value="festa">Evento Festivo</option>
            <option value="consulta">Consulta Médica</option>
          </select-input>
          <div class="footer">
            <button-air v-if="!isEdit" @click.native="showModal" class="button-air" estilo="secundario">Cancelar</button-air>
            <button-air v-if="isEdit" @click.native="deleteEvent" class="button-air" estilo="icone">Excluir</button-air>
            <button-air v-if="!isEdit" @click.native="addEvent">Confirmar</button-air>
            <button-air v-if="isEdit" @click.native="editOk">Editar</button-air>
          </div>
        </form>
      </form-modal>
    </div>
    <div @click="showModal()" class="close-modal" :class="classModal"></div>
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
      //Estados para manipulação da view
      defaultSelect: '',
      updateIndex: '',
      classModal: '',
      closeModal: '',
      actualOption: '',
      isEdit: false,
      //Objeto evento para pegar os dados do Form com two-way data binding
      evento: {
        id: 0,
        title: '',
        local: '',
        start: '',
        end: '',
        color: '',
        type: ''
      },
      //Array de eventos recebido pelo componente Full Callendar
			eventsData: [],
      //Configurações de renderização recebidos pelo Full Callendar
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
    //Metodo para limpar os campos de Adição / Edição do formulario
    clearData () {
      this.evento.title = '';
      this.evento.local = '';
      this.evento.start = '';
      this.evento.end = '';
      this.evento.color = '';
      this.defaultSelect = false;
    },
    //Metodo para adicionar um novo evento no array incrementando a variavel id e chamando o metodo para esconder o modal
    addEvent() {
      this.increment();
      this.eventsData.push(Object.assign({}, this.evento));
      this.showModal();
    },
    //Metodo disparado ao clicar em um evento no formulario recebendo o evento e passando para o objeto evento
    editEvent(eventoRec) {
      if(eventoRec.end) {
        this.isEdit = true;
        this.evento.title = eventoRec.title;
        this.evento.local = eventoRec.local;
        this.evento.start = eventoRec.start._i;
        this.evento.end = eventoRec.end._i;
        this.actualOption = eventoRec.type;
        this.updateIndex = this.eventsData.map(eventData => eventData.id).indexOf(eventoRec.id);
        this.showModal();
      } else {
        this.isEdit = true;
        this.evento.title = eventoRec.title;
        this.evento.local = eventoRec.local;
        this.evento.start = eventoRec.start._i;
        this.actualOption = eventoRec.type;
        this.updateIndex = this.eventsData.map(eventData => eventData.id).indexOf(eventoRec.id);
        this.showModal();
      }
    },
    //Metodo para confirmar a edição do evento, deletando o existente no array e criando um novo
    editOk () {
      this.eventsData.splice(this.updateIndex, 1);
      this.addEvent();
    },
    //Metodo para remover um evento no array
    deleteEvent() {
      const removeIndex = this.eventsData.map(eventData => eventData.id).indexOf(this.evento.id);
      this.eventsData.splice(removeIndex, 1);
      this.showModal();
    },
    //Metodo para incrementar o ID
    increment () {
      this.evento.id ++;
    },
    //Metodo para definir o tipo de evento e passar a cor na renderização da view
    tipoEvento (tipo) {
      this.evento.type = tipo;
      if(tipo == 'reuniao') {
        this.evento.color = 'green'
      } else if(tipo == 'festa') {
        this.evento.color = 'red'
      } else if(tipo == 'consulta') {
        this.evento.color = 'blue'
      } else {
        this.evento.color = 'black'
      }
    },
    //Metodo para Mostrar o Modal de Formulario
    showModal () {
      if (this.classModal !== 'show') {
        this.classModal = 'show'
        this.closeModal = 'show'
      } else {
        this.classModal = ''
        this.closeModal = ''
        this.clearData();
        this.isEdit = false;
        this.actualOption = "";
      }
    }
  }
}
</script>

<style <style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  position: relative;

  .modal-1 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    visibility: hidden;
    z-index: 10;
    // visibility: visible;
  }

  .close-modal {
  content: "";
  z-index: 9;
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  background-color: transparent;
  background-color: rgba(0, 0, 0, 0.75);
  visibility: hidden;
  right: 0;
}

.show {
    visibility: visible;
  }
}
</style>

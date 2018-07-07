<template>
  <div>
    <full-calendar :config="config" :events="events"/>
  </div>
</template>

<script>
import moment from 'moment'
import 'fullcalendar/dist/locale/pt-br'
	export default {
  data () {
    return {
			events: [
				{
            title  : 'event1',
            start  : '2018-07-01',
        },
        {
            title  : 'event2',
            start  : '2018-07-05',
            end    : '2018-07-07',
        },
        {
            title  : 'event3',
            start  : '2018-07-05T12:30:00',
            allDay : false,
        },
			],
			config: {
        defaultView: 'month',
				locale: 'pt-br',
				editable: false,
				eventRender: function(event, element) {
        	console.log(event)
    		}
      },
    }
  }
}
</script>

<style>

</style>
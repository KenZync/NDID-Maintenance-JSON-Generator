<script setup lang="ts">
import { computed, ref } from 'vue'
import Datepicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'

defineProps<{ msg: string }>()

const date = ref<Date[]>([new Date(), new Date()]);

const hasUpdated = ref(false);

const start = ref(date.value[0])
const end = ref(date.value[1])

const handleDate = () => {
  hasUpdated.value = true
  start.value =  date.value[0]
  end.value = date.value[1]
}

const epochTime = (time: Date) => {
  return Math.floor(time.getTime()/1000.0)
}

const dayMonthYear = (time:Date) => {
  return time.toLocaleDateString('th-TH', {year: 'numeric', month: 'long', day: 'numeric'})
}

const timeShort = (time: Date) => {
  return time.toLocaleTimeString('th-TH', {timeStyle: 'short'})

}

const weekDay = (time: Date) => {
  return time.toLocaleDateString('th-TH', {weekday: 'long'})
}

const dayMonth = (time:Date) => {
  return time.toLocaleDateString('th-TH', {month: 'long', day: 'numeric'})
}

const generate = async () => {
  const data = `"idps_bcp": {
	"start_time": `+epochTime(start.value)+`,
	"end_time": `+epochTime(end.value)+`,
	"title": "NDID ปิดทำการชั่วคราว",
	"description": "NDID ปิดปรับปรุงระบบใน`+weekDay(start.value)+`ที่ `+dayMonth(start.value)+` เวลา `+timeShort(start.value)+` น. - `+weekDay(end.value)+`ที่ `+dayMonth(start.value)+` เวลา `+timeShort(end.value)+` น. ขออภัยในความไม่สะดวก"
}`
  await navigator.clipboard.writeText(data);
  alert('Copied JSON to clipboard, use ctrl v to paste anywhere.');
}

</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <Datepicker v-model="date" range multiCalendars locale="th" @update:modelValue="handleDate"/>
    <pre></pre>
    <div  v-if="hasUpdated">
      <div>
          ปิด {{weekDay(start)}}ที่ {{dayMonthYear(start)}}
          เวลา {{timeShort(start)}}
      </div>
      <div>
        ถึง {{weekDay(end)}}ที่ {{dayMonthYear(end)}}
          เวลา {{timeShort(end)}}
      </div>
      <div>
        start_time : {{epochTime(start)}}
      </div>
      <div>
        end_time : {{epochTime(end)}}
      </div>
      <div>title : NDID ปิดทำการชั่วคราว</div>
      <div>description : NDID ปิดปรับปรุงระบบใน{{weekDay(start)}}ที่ {{dayMonth(start)}} เวลา {{timeShort(start)}} น. - {{weekDay(start)}} เวลา {{timeShort(start)}} น. ขออภัยในความไม่สะดวก</div>
      <pre></pre>
      <button type="button" @click="generate">Copy JSON to clipboard</button>
    </div>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}


</style>

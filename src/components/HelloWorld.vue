<template>
  <div>
    <date-picker
      v-model="value1"
      format="YYYY-MM-DD dddd"
      type="date"
      placeholder="開始時間"
      :disabled-date="disabledBeforeTodayAndValue2EndDay"
    >
    </date-picker>
    <date-picker
      v-model="value2"
      format="YYYY-MM-DD dddd"
      type="date"
      placeholder="結束時間"
      :disabled-date="disabledBeforeToday"
    >
    </date-picker>
    <date-picker
      v-model="time1"
      :minute-step="10"
      format="a HH:mm"
      type="time"
      placeholder="HH:mm a"
    ></date-picker>

    <date-picker
      v-model="time2"
      :minute-step="10"
      format="a HH:mm"
      type="time"
      placeholder="HH:mm a"
    ></date-picker>
    <button @click="printConsole()">按我一下</button>
  </div>
</template>

<script>
const dayjs = require('dayjs');
const birthday = new Date('March 13, 08 04:20');
console.log(birthday.getHours());
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';
import 'vue2-datepicker/locale/zh-cn';
export default {
  name: 'optionTest',
  data: () => ({
    value1: null,
    value2: '2022-11-15',
    time1: 'March 13, 08 04:20',
    time2: 'March 13, 08 04:20',
  }),
  components: {
    DatePicker,
  },
  methods: {
    disabledBeforeTodayAndValue2EndDay(date) {
      const today = new Date();
      today.setHours(0, 0, 0, 0);
      return date < today || date > this.value2;
    },
    disabledBeforeToday(date) {
      const today = new Date();
      today.setHours(0, 0, 0, 0);
      return date < today || date <  (this.value1 ? this.value1 : "2100-11-15");
    },

    beforeEndTime(date) {
      return date.getHours() < this.time2.getHours();
    },
    printConsole() {
      console.log('value1:', this.value1, 'value2:', this.value2);
      console.log(
        'value1:',
        dayjs(this.value1).format('YYYY-MM-DD'),
        'value2:',
        dayjs(this.value2).format('YYYY-MM-DD')
      );
    },
  },
};
</script>

<style lang="scss" scoped></style>

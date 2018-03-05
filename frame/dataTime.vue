<template>
    <mt-datetime-picker
        v-model="pickerVisible"
        @confirm="handleConfirm"
        @cancel="cancelFn"
        type="date"
        year-format="{value} 年"
        month-format="{value} 月"
        date-format="{value} 日"
        :visible.sync="pickerVisible"
        ref='timeDom'
    >
    </mt-datetime-picker>
</template>

<script>
import Vue from 'vue'
import { DatetimePicker } from 'mint-ui';
Vue.component(DatetimePicker.name, DatetimePicker);
export default {
    name: 'dataTime',
    data () {
        return {
            pickerVisible: false
        }
    },
    methods: {
      openPicker() {
        this.$refs.picker.open();
      },
      handleConfirm (val) {
          this.$emit('closeData',val)
      },
      cancelFn () {
          this.$emit('closeData')
      }
    },

}
</script>

<style lang='scss' scoped>
    .data-box{
        width:100%;
    }
    .picker-items{
        background: red;
        .picker-slot-center:nth-child(3){
            display: noe!important;
        }
    }
    .picker-slot.picker-slot-center{
        background: red;
    }
</style>

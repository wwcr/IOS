<template>
    <div class="calculator-box">
        <div class="btn-box">
            <button class="cancel-btn" @click="cancelTime(0)">取消</button>
            <button class="sure-btn" @click="cancelTime(1)">确定</button>
        </div>
        <mt-picker :slots="Slots" @change="onValuesChange"></mt-picker>
    </div>
</template>

<script>
import Vue from 'vue'
import { Picker } from 'mint-ui';
Vue.component(Picker.name, Picker);
export default {
    name: 'calculatorPicker',
    data () {
        return {
            Slots: [ //寻车期限(mint-ui)
                {
                    flex: 1,
                    values: ['0年', '1年', '2年','3年', '4年', '5年','6年', '7年', '8年','9年', '10年', '11年','12年', '13年', '14年','15年', '16年', '17年','18年', '19年', '20年','21年', '22年', '23年', '24年', '25年','26年', '27年', '28年', '29年', '30年'],
                    className: 'slot1',
                    textAlign: 'center'
                },
                {
                    flex: 1,
                    values: ['0月', '1月', '2月','3月', '4月', '5月','6月', '7月', '8月','9月', '10月', '11月'],
                    className: 'slot2',
                    textAlign: 'center'
                }
            ],
            calculatorValue: []
        }
    },
    methods: {
        onValuesChange(picker, values) {//寻车期限（mint-ui）
            // console.log(picker, values)
            this.calculatorValue = values
            // if (values[0] > values[1]) {
            //     picker.setSlotValue(1, values[0]);
            // }
        },
        cancelTime (val){ //寻车期限滑块取消按钮
            this.$emit('closePicker', {value:this.calculatorValue, id: val})
        }
    }
}
</script>

<style scoped lang='scss'>
    .calculator-box{
        background: #fff;
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        padding: .2rem 0;
        .btn-box{
            display: flex;
            justify-content: space-between;
            button{
                width: 2rem;
                height: 1rem;
                font-size: .5rem;
                margin: 0 .5rem;
                border: 0;
                background:#fff;
                color: #4088ff;
            }
        }
    }
</style>

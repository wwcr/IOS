<template>
    <div class="card-gps-mark">
        <div class="gps-box">
            <div class="btn-box">
                <button class="cancel-btn" @click="cancelTime(0)">取消</button>
                <button class="sure-btn" @click="cancelTime(1)">确定</button>
            </div>
            <mt-picker :slots="gspSlots" @change="onValuesChange"></mt-picker>
        </div>
    </div>
</template>

<script>
import Vue from 'vue'
import { Picker } from 'mint-ui';
Vue.component(Picker.name, Picker);
export default {
    name: 'gpsPicker',
    data () {
        return {
            gspSlots: [
                {
                    flex: 1,
                    values: ['否', '是'],
                    className: 'gspSlots',
                    textAlign: 'center'
                }
            ],
            gpsValue: ''
        }
    },
    methods: {
        onValuesChange(picker, values) {
            // console.log(picker, values)
            this.gpsValue = values[0]
            // if (values[0] > values[1]) {
            //     picker.setSlotValue(1, values[0]);
            // }
        },
        cancelTime (val){ //取消按钮
            this.$emit('closePicker', {gps:this.gpsValue, id: val})
        }
    }
}
</script>

<style scoped lang='scss'>
    .card-gps-mark{
        position: fixed;
        top:0;
        left:0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, .5);
        z-index: 1000;
    }
    .gps-box{
        background: #fff;
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        padding-bottom: .5rem;
        .btn-box{
            display: flex;
            justify-content: space-between;
            background: #eaeaea;
            button{
                width: 2rem;
                height: 1rem;
                font-size: .5rem;
                margin: 0 .5rem;
                border: 0;
                background: #eaeaea;
            }
        }
    }
</style>

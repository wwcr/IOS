<template>
	<div class="carcalculator-page">
		<div class="money-limit">
			<div class="li">
				<label>贷款总额</label>
				<input 
					type="text"
					pattern="[0-9]*"
					placeholder="0" 
					style="position:relative;
						top:0.2rem;"
					@input= 'getMoneyVal'
					v-model="form.money">
				<span>万元</span>
			</div>
			<div class="li large">
				<label>贷款期限</label>
				<i>
					<input 
						type="text" 
						placeholder="0" 
						readonly
						unselectable="on" onfocus="this.blur()"
						v-model="form.month"
						style="position:relative;
						top:-.01rem;"
						@click="openCalculator">
					<span><img src="../../../assets/img/down-jt.jpg" alt=""></span>
				</i>
			</div>
			<div class="li large">
				<label>贷款年利率</label>
				<input 
					type="number" 
					placeholder="0" 
					@input= 'getMoneyVal'
					v-model="form.li">
				<span>%</span>
			</div>
		</div>
		<div class="principal-interest-page">
			<div class="nav-bar-box">
				<div class="nav-bar" :class="{navActive: currentID == 2}" @click='tab(2)'>等额本息</div>
				<div class="nav-bar"  @click='tab(1)' :class="{navActive: currentID == 1}">等额本金</div>
			</div>
			<!-- 等额本息 -->
			<div class="principal-box" v-if='currentID == 2'>
				<ul class="principal-content" >
					<li>
						<label>月还贷款(元)</label>
						<span v-if='typeof (somemoney.each_money) == "number"' class="text-right">{{somemoney.each_money.formatMoney()}}</span>
						<span v-else>{{somemoney.each_money}}</span>
					</li>
					<li>
						<label>支付利息金额(元)</label>
						<span v-if='typeof (somemoney.all_li) == "number"' class="text-right">{{somemoney.all_li.formatMoney()}}</span>
						<span v-else>{{somemoney.all_li}}</span>
					</li>
					<li>
						<label>还款总额(元)</label>
						<span v-if='typeof (somemoney.all_money) == "number"' class="text-right">{{somemoney.all_money.formatMoney()}}</span>
						<span v-else>{{somemoney.all_money}}</span>
					</li>
				</ul>
			</div>
			<!-- 等额本金 -->
			<div class="principal-box" v-if='currentID == 1'>
				<ul class="principal-content">
					<li>
						<label>首月还贷款(元)</label>
						<span v-if='typeof (somemoney.first) == "number"' class="text-right">{{somemoney.first.formatMoney()}}</span>
						<span v-else>{{somemoney.first}}</span>
					</li>
					<li>
						<label>逐月递减(元)</label>
						<span v-if='typeof (somemoney.each_reduce) == "number"' class="text-right">{{somemoney.each_reduce.formatMoney()}}</span>
						<span v-else>{{somemoney.each_reduce}}</span>
					</li>
					<li>
						<label>支付利息总额(元)</label>
						<span v-if='typeof (somemoney.all_li) == "number"' class="text-right">{{somemoney.all_li.formatMoney()}}</span>
						<span v-else>{{somemoney.all_li}}</span>
					</li>
					<li>
						<label>还款总额 (元)</label>
						<span v-if='typeof (somemoney.all_money) == "number"' class="text-right">{{somemoney.all_money.formatMoney()}}</span>
						<span v-else>{{somemoney.all_money}}</span>
					</li>
				</ul>
			</div>
		</div>
		<calculatorPicker
			v-if='calculatorFlag'
			@closePicker = 'closePicker'
		/>
	</div>
</template>

<script>
import units from '@/tools/units'
import calculatorPicker from '@/components/frame/calculatorPicker'
export default {
	name: 'carcalculator',
	data () {
		return {
			currentID: 2,
			calculatorFlag: false,
			limitYearVal: '',
			limitMonthVal: '',
			eachmonth: '',
			form: {
				money: '',//贷款总额
				li: '',//贷款年利率
				month: '30年（360期）',//贷款期限
				limit: 360//贷款总月
			},
			// someRate: {
			// 	each_money: '---',
			// 	all_li: '---',
			// 	all_money: '---'
			// },
			somemoney: {
				each_money: '---',
				first: '---',
				all_li: '---',
				all_money: '---',
				each_reduce: '---'
			}
		}
	},
	watch:{
		'form.money': function(newVal,oldVal){
			const regex =  /^[0-9]*$/;
			if(!regex.test(newVal)) {//如果小于等于零
				this.form.money = oldVal //恢复原值
			}
		}
	},
	methods: {
		getMoneyVal() {
			// console.log(22222,11)
			let {
				money,
				limit,
				li
			} = this.form
			if(money != ''&&li != '') {
				this.$http.post(units.host('car_loan', 'api'), {
					money: money*10000,
					li: li*0.01,
					month: limit,
					type: this.currentID  //1等额本金  2等额本息
				}).then(function (res) {
					this.somemoney = res.body
				});
			} else {
				this.somemoney = {
					each_money: '---',
					first: '---',
					all_li: '---',
					all_money: '---',
					each_reduce: '---'
				}
			}
		},
		tab (id) {
			this.currentID = id
			let {
				money,
				limit,
				li
			} = this.form

			if(money != ''&&li != '') {
				this.$http.post(units.host('car_loan', 'api'), {
					money: money*10000,
					li: li*0.01,
					month: limit,
					type: id  //1等额本金  2等额本息
				}).then(function (res) {
					this.somemoney = res.body
				});
			}
			
		},
		openCalculator () {
			this.calculatorFlag = true
		},
		closePicker (obj) {
			if (obj.id == 0) {
				this.form.limitVal = ''
			} else {
				if( obj.value[0] == '0年') {
					this.limitYearVal = ''
				} else {
					this.limitYearVal = obj.value[0]
				}
				if(obj.value[1] == '0月') {
					this.eachmonth = ''
				}else {
					this.eachmonth = obj.value[1]
				}
				this.limitMonthVal = obj.value[0].split('年')[0] * 12 + obj.value[1].split('月')[0]*1
				this.form.month = this.limitYearVal + this.eachmonth + '(' + this.limitMonthVal + '期)'
				console.log(obj.value[1])
				this.form.limit = this.limitMonthVal
			}
			this.calculatorFlag = false
		}
	},
	created () {
		units.title.set('车贷计算器');
		
		// console.log(this)
		// this.$http.post(units.host('car_loan', 'api'), {
		// 	money: 10000,
		// 	li: 1,
		// 	month: 10,
		// 	type: 2 //1等额本金  2等额本息
		// }).then(function (res) {
		// 		this.someRate = res.body 
        // });
	},
	components: {
		calculatorPicker
	}
}
</script>

<style scoped lang='scss'>
	i{
		font-style: normal;
	}
	.text-right{
		text-align: right;
		padding-right:.3rem;
		box-sizing: border-box; 
	}
	.carcalculator-page{
		background: #f0f4fa;
		padding-top: 1.25rem;
		font-size: .45rem;
		.money-limit{
			background: #fff;
			padding: 0 .4rem;
			box-sizing: border-box;
			margin-top: .3rem;
			.li{
				border-bottom: .01rem solid #f0f0f0;
				line-height: 1.3rem;
				display: flex;
				label{
					flex:3
				}
				span{
					flex:1.2;
					text-align:right;
					img{
						width: .4rem;
						position: relative;
						top: -.1rem;
					}
				}
				input{
					flex:6;
					// border: .01rem solid #ccc;
					text-align: right;
					line-height: 1rem;
					// padding-right: .2rem;
					height: 1rem;
					position: relative;
					top: .18rem;
				}
			}
			.large{
				label{
					flex:7;
				}
				input{
					flex: 8;
				}
			}
		}
	}
	.principal-interest-page{
		margin-top: .3rem;
		background: #fff;
		padding: 0 .3rem;
		box-sizing: border-box;
		.nav-bar-box{
			padding-top: .3rem;
			display:flex;
			.nav-bar{
				text-align: center;
				width: 50%;
				height: 1.1rem;
				line-height: 1.1rem;
				border: 1px solid #297aff;
				border-radius: 6px;
				background: #f8f9fa;
				color: #297aff;
				&:nth-child(1){
					border-top-right-radius: 0;
					border-bottom-right-radius: 0;
					border-right: 0;
				}
				&:nth-child(2){
					border-top-left-radius: 0;
					border-bottom-left-radius: 0;
				}
			}
			.navActive{
				background: #297aff;
				color:#fff;
			}
		}
	}
	.principal-content{
		padding-bottom: .8rem;
		li{
			margin-top: .5rem;
			display:flex;
			label{
				flex:1;
			}
			span{
				flex:1;
				padding-left: 1rem;
			}
		}
	}
</style>

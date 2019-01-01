<template>
	<div class="index">
		<el-container class="c-outer">
	
			<!-- <el-header class="c-header">
				<span>首页</span>
				<span class="logout pull-right">退出</span>
			</el-header> -->
			<Header title="首页"></Header>
		  	<el-main class="c-main">
		  		<div class="main-in">
		  			<el-button-group>
					  	<el-button type="primary" :plain="type != 1" class="btn-100" @click="clickType(1)">今天</el-button>
					  	<el-button type="primary" :plain="type != 2" class="btn-100" @click="clickType(2)">昨天</el-button>
					  	<el-button type="primary" :plain="type != 3" class="btn-100" @click="clickType(3)">本月</el-button>
					</el-button-group>
					<el-row>
						<el-col :span="24" class="index-item">
							<el-date-picker
								class="index-time"
						      	v-model="value1"
						      	type="datetime"
						      	placeholder="开始时间"
						      	@change="changeTime"
						    >
						    </el-date-picker>
						</el-col>
						<el-col :span="24" class="index-item">
							<el-date-picker
								class="index-time"
						      	v-model="value2"
						      	type="datetime"
						      	placeholder="结束时间"
						      	@change="changeTime"
						    >
						    </el-date-picker>
						</el-col>
						<el-col :span="24" class="index-item">
							<el-button type="primary" class="btn-300" @click.native="init">查询</el-button>
						</el-col>
						<el-col :span="24" class="index-item">
							<p>
								<span class="index-num">{{VisitUserNumber}}</span>	
							</p>
							<span>
								访问用户数
							</span>
						</el-col>

						<el-col :span="24" class="index-item">
							<p>
								<span class="index-num">{{RegUserNumber}}</span>	
							</p>
							<span>
								注册用户数
							</span>
						</el-col>

						<el-col :span="24" class="index-item">
							<p>
								<span class="index-num">{{ApprovalUserNumber}}</span>	
							</p>
							<span>
								成交用户数
							</span>
						</el-col>
						  	
						
					</el-row>	

		  		</div>
				

		  	</el-main>
			
		</el-container>
		
		


	</div>
</template>

<script>
import Header from './Header'
export default {
	components:{
	// Button,Field
		Header
	},
	name: 'Index',
	data () {
		return {
			type: 3,
			value1: '',
			value2: '',
			VisitUserNumber: 1000,
			RegUserNumber: 0,
			ApprovalUserNumber: 0,
		}
	},
	mounted () {
		this.clickType(3)
	},
	methods:{

		changeTime() {
			console.log(this.value1)
		},

		clickType(type) {
			this.type = type
			const time = new Date()
			const year = time.getFullYear()
			const month = time.getMonth()
			const day = time.getDate()
			const hour = time.getHours()
			const min = time.getMinutes()
			const sec = time.getSeconds()
			let start
			let end
			if (type == 1) {
				start = new Date(year, month, day, 0, 0, 0)
				end = time
			} else if (type == 2) {
				end = new Date(year, month, day, 0, 0, 0)
				start = new Date(end.getTime() - 24*3600*1000)
			} else if (type == 3) {
				start = new Date(year, month, 1, 0, 0, 0)
				end = time
			}
			console.log(start)
			console.log(end)
			this.value1 = start
			this.value2 = end
			this.init()
		},

		format(time) {
   			if (time) {
				const year = time.getFullYear()
				const month = parseInt(time.getMonth()+1)>=10?parseInt(time.getMonth()+1):'0'+parseInt(time.getMonth()+1)
				const day = parseInt(time.getDate())>=10 ? parseInt(time.getDate()) : '0'+ parseInt(time.getDate())
				const hour = parseInt(time.getHours())>=10? parseInt(time.getHours()): '0'+parseInt(time.getHours())
				const min = parseInt(time.getMinutes())>=10? parseInt(time.getMinutes()): '0'+parseInt(time.getMinutes())
				const sec = parseInt(time.getSeconds())>=10? parseInt(time.getSeconds()): '0'+parseInt(time.getSeconds())
				return year+'-'+month+'-'+day+' '+hour+':'+min+':'+sec
   			}
		},

		init() {
			const {
				value1,
				value2,
			} = this
			if (!value1 || !value2) {
				this.warn("请选择时间！")
				return
			}
			const StartDateTime = this.format(value1)
			const EndDateTime = this.format(value2)
			const param = {
				StartDateTime,
				EndDateTime,
			}
			this.pp('GetStatistics', param, res => {
				if (res.ret) {
					const {
						VisitUserNumber,
						RegUserNumber,
						ApprovalUserNumber,
					} = res.data
					this.VisitUserNumber = VisitUserNumber
					this.RegUserNumber = RegUserNumber
					this.ApprovalUserNumber = ApprovalUserNumber
				} else {
					this.warn(res.msg)
				}
			})
		},

	},
}

</script>

<style scoped>
.index {
	position: absolute;
	top: 0px;
	left: 0px;
	right: 0px;
	bottom: 0px;
	overflow: hidden;
	vertical-align: middle;
}
.table-outer {
	width: 1000px;
	height: calc(100% - 100px);
	margin: 20px auto;
}
.index-table {
	height: 100%;
	width: 100%;
	max-width: 1000px;
	margin: 0 auto;
	margin-top: 20px;
	text-align: left;
}
.index-bottom {
	width: 100%;
	margin: 10px auto;
	text-align: cneter;
}
.index-bottom-page {
	padding: 0px 10px;
}
.op-item {
	height: 60px;
	width: 500px;
	line-height: 60px;
	margin: 0 auto;
	margin-top: 20px;
	border-radius: 5px;
	position: relative;
    color: #67c23a;
    background: #f0f9eb;
	border: 1px solid #c2e7b0;
	padding: 0 15px;
	cursor: pointer;
}
.op-item-icon {
	font-size: 18px;
}
.c-main {
	text-align: center;
}
.main-in {
	width: 300px;
	text-align: center;
	margin: 0 auto;
}
.index-item {
	margin-top: 20px;
}
.index-time {
	width: 100%;
}
.btn-300 {
	width: 300px;
}
.index-num {
	display: inline-block;
	width: 50px;
	height: 50px;
	line-height: 50px;
	border-radius: 25px;
	background-color: #409eff;
	color: #ffffff;
	font-size: 20px;
	font-weight: bold;
}



</style>

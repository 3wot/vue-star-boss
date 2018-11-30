<template>
	<div class="index">
		<el-container class="c-outer">
	
			<!-- <el-header class="c-header">
				<span>首页</span>
				<span class="logout pull-right">退出</span>
			</el-header> -->
			<Header title="首页"></Header>
		  	<el-main class="c-main">
				<div class="op-item" @click="gotoValuation">
					<span class="pull-left op-item-icon">
						<i class="el-icon-menu"></i>
					</span>
					<span>估值</span>
					<span class="pull-right op-item-icon">
						<i class="el-icon-arrow-right"></i>
					</span>
				</div>
				<div class="op-item" @click="gotoFirstCheck">
					<span class="pull-left op-item-icon">
						<i class="el-icon-menu"></i>
					</span>
					<span>初审</span>
					<span class="pull-right op-item-icon">
						<i class="el-icon-arrow-right"></i>
					</span>
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
			
		}
	},
	mounted () {
		
	},
	methods:{
		
		// 估值
		gotoValuation() {
			this.$router.push({ name : 'valuation' })
		},
		// 初审
		gotoFirstCheck() {
			this.$router.push({ name : 'firstCheck' })
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




</style>

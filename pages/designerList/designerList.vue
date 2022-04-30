<template>
	<view class="list-box">
		<lsf-designerItem></lsf-designerItem>
		<text class="list-line">--- 已经到底了 ---</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		onLoad: function (option) { //option为object类型，会序列化上个页面传递的参数
				console.log(option.type); //打印出上个页面传递的参数。
				uni.setNavigationBarTitle({
					title: `${option.type}风格`
				})
				
			}
	}
</script>

<style lang="less">
.list-box {
	box-sizing: border-box;
	width: 100%;
	min-height: 100vh;
	background-color: #f3f5f7;
	padding: 1px 20rpx;
	padding-bottom: 20rpx;
}
.list-line {
	text-align: center;
	width: 100%;
	display: inline-block;
	margin-top: 10rpx;
}
</style>

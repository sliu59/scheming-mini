<template>
	<view class="design-container">
		<view class="view-list">
			<view class="view-item" v-for="(item,index) in designerList" :key="index" @click="toDetail(item)">
				
				<lsf-card 
					:src="item.avatar" 
					:radius="'20rpx'" 
					full 
					:title="item.name" 
					:tag="item.desc"
					:headerLine="true"
					:imageRadius="'100%'"
					>
					<view class="fui-card__content ">
						<image class="case-img" :src="item.image" mode="scaleToFill"></image>
					</view>
				</lsf-card>
				
			</view>
		</view>
	</view>
</template>

<script>
	import {designerList} from '@/static/designers.js'
	export default {
		name:"designerItem",
		data() {
			return {
				designerList: designerList
			};
		},
		mounted() {
			console.log(this.designerList);
		},
		methods: {
			toDetail(data) {
				console.log(data);
				var data = JSON.stringify(data); // 这里转换成 字符串
					uni.navigateTo({
						url:'../packageDetail/packageDetail?data='+data
				})
			}
		},
	}
</script>

<style lang="less">

.view-list {
	box-sizing: border-box;
	
	.view-item {
		margin-top: 30rpx;
		.fui-card__content {
			padding: 10rpx 20rpx;
			.case-img {
				width: 100%;
			}
		}
	}
}
</style>
<template>
	<view class="design-container">
		<view class="view-list">
			<view class="view-item" >
				
				<lsf-card 
					:src="packageDetail.avatar" 
					:radius="'20rpx'" 
					full 
					:title="packageDetail.name" 
					:tag="packageDetail.desc"
					:headerLine="true"
					:imageRadius="'100%'"
					>
					<view class="fui-card__content ">
						<image class="case-img" :src="packageDetail.package.packImg" mode="widthFix"></image>
						<uni-table border stripe emptyText="暂无更多数据" >
							<!-- 表头行 -->
							<uni-tr>
								<uni-th align="center" width="70">产品包内容</uni-th>
								<uni-th align="center">规格</uni-th>
								<uni-th align="center">适合面积</uni-th>

							</uni-tr>
							<!-- 表格数据行 -->
							<uni-tr v-for="(item,index) in packageDetail.package.list" :key="index">
								<uni-td>{{item.name}}</uni-td>
								<uni-td>{{item.format}}</uni-td>
								<uni-td>{{item.suitArea}}</uni-td>
							</uni-tr>
						
						</uni-table>
						<text class="total-section">总价: {{packageDetail.package.total}}</text>
						<button class="uni-button"   @tap="appLoginWx" type="Primary">进入下单界面</button>
						<button class="uni-button"  type="info">联络设计师，专人服务</button>
						
					</view>
				</lsf-card>
				
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"packageDetail",
		data() {
			return {
				packageDetail: {}
			};
		},
		onLoad(options) {
			var packageDetail = JSON.parse(options.data); // 字符串转对象
					console.log(packageDetail)
					this.packageDetail = packageDetail
		},
		methods: {
			// js 部分
			appLoginWx(){
				uni.getUserProfile({  
				        lang: 'zh_CN',
				        desc:'获取用户信息',
				        success: userInfo=> {
				            console.log(userInfo,'userInfo');
				            uni.login({
				                provider: 'weixin',
				                success: loginInfo=> {
				                    console.log(loginInfo,'loginInfo');     
				                }
				            });
				         },
				        fail:err=>{
				            console.log(err,'err')
				        }
				    });
			}
		}
		
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
.total-section {
	display: inline-block;
	margin-top: 20rpx;
}
.uni-button {
	margin-top: 20rpx;
}
</style>
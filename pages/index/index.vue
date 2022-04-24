<template>
	<view class="content">
		<!-- <image class="bg" src="/static/1.jpg"></image> -->
		<swiper 
			class="swiper" 
			:autoplay="false" 
			:interval="5000" 
			:duration="300" 
			:current="swiperCurrent" 
			@change="changeSwiper"
			:indicator-dots="false"
			>
			<swiper-item v-for="(item,index) in swiperList.homeImageDesc" :key="index">
				<image class="swiper-item" :src="item.url" mode=""></image>
			</swiper-item>
		</swiper>
			<!-- 风格对应文案 -->
			<view class="type-desc">
				
				<view v-for="(item,index) in swiperList.desc" :key="index">{{item}}</view>
			</view>
		    <!-- 轮播指示点样式修改 -->
		    <view class="dots">
		          <block v-for="(item,index) in swiperList.homeImageDesc" :key="index">
		              <view class="dot" :class="index==swiperCurrent ? ' active' : ''">{{item.name}}</view>
		          </block>
		      </view>
		<view class="text-area">
			<view>
				<div class="selectButton" @click="open">
					<image src="../../static/switch.png" mode="" class="switch"></image>

					<text>{{swiperList.type}}</text>
				</div>
					<uni-popup class="popup-section" ref="popup" type="bottom" background-color="#fff">
						<text class="popup-title">风格切换</text>
						<view class="popup-content">
							<view :class="item.isActive? 'isActive':''" @click="itemClick(item)" class="radio-item" v-for="(item,index) in styleData" :key="index">
								<text>{{item.type}}</text>
							</view>
						</view>
						<view class="set-bottom"></view>
						<view class="popup-bottom">
							<view class="bottom-button set-line" @click="close()">取消</view>
							<view class="bottom-button set-color" @click="comfirmStyle">确认</view>
						</view>
					</uni-popup>
				</view>
		</view>
	</view>
</template>

 <script>
	export default {
		data() {
			return {
				title: 'Hello',
				current: 0,
				swiperCurrent: 0,
				swiperList: {
						type:'欧式',
						desc: [
							'北欧风格',
							'色彩缤纷、快乐宁静',
							'简单富有设计感',
							'特别美好'
						],
						isActive: true,
						homeImageDesc: [
							{
								name:'客厅',
								// url: '/static/page1/1.jpg',
								url: 'https://pic.underrate.net/app20220424/1.jpg',
								
							},{
								name:'卧室',
								// url: '/static/page1/2.jpg',
								url: 'https://pic.underrate.net/app20220424/2.jpg',
								
								
							},
							{
								name:'餐厅',
								// url: '/static/page1/3.jpg',
								url: 'https://pic.underrate.net/app20220424/3.jpg',
								
							}
						]
					},
				styleData: [
					{
						type:'欧式',
						isActive: true,
						desc: [
							'北欧风格',
							'色彩缤纷、快乐宁静',
							'简单富有设计感,特别美好'
						],
						homeImageDesc: [
							{
								name:'客厅',
								// url: '/static/page1/1.jpg',
								url: 'https://pic.underrate.net/app20220424/1.jpg',
								
							},{
								name:'卧室',
								// url: '/static/page1/2.jpg',
								url: 'https://pic.underrate.net/app20220424/2.jpg',
								
								
							},
							{
								name:'餐厅',
								// url: '/static/page1/3.jpg',
								url: 'https://pic.underrate.net/app20220424/3.jpg',
								
							}
						]
					},
					{
						type:'japandi',
						desc: [
							'japandi',
							'粗陶、自然、浑然天成',
							'天然的色调',
							'舒心的空间'
						],
						isActive: false,
						homeImageDesc: [
							{
								name:'客厅',
								// url: '/static/page2/1.jpg',
								url: 'https://pic.underrate.net/app20220424/4.jpg',
								
							},{
								name:'卧室',
								// url: '/static/page2/2.jpg',
								url: 'https://pic.underrate.net/app20220424/5.jpg',
								
							},{
								name:'餐厅',
								// url: '/static/page2/3.jpg',
								url: 'https://pic.underrate.net/app20220424/6.jpg',
								
							}
						]
					}
					
				]
			}
		},
		onLoad() {
			console.log(this.swiperList)
		},
		methods: {
		// 打开弹出层
		open(){
		        // 通过组件定义的ref调用uni-popup方法 ,如果传入参数 ，type 属性将失效 ，仅支持 ['top','left','bottom','right','center']
		        this.$refs.popup.open('bottom')
		},
		close() {
			this.$refs.popup.close()
		},
		// 点击风格
		itemClick(item) {
			console.log(item)
			this.styleData.forEach(i => {
				i.isActive = false
			})
			item.isActive = true
		},
		// 确定风格
		comfirmStyle() {
			this.styleData.map(item => {
				if(item.isActive === true) {
					this.swiperList = item
				}
			})
			this.$refs.popup.close()
			console.log(this.swiperList)
		},
		changeSwiper(e) {
			this.swiperCurrent = e.detail.current;
		}
		}
	}
 </script>

<style lang="less">
	.content {
		/* padding-top: 100rpx; */
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		.dots {
		          position: absolute;
		          top: 170rpx;
		          right: 40rpx;
		          // 这里一定要注意兼容不然很可能踩坑          
		          // transform: translate(-50%, 0);
		          // -webkit-transform: translate(-50%, 0);        
		          z-index: 99;
		          display: flex;
		          flex-direction: row;
		          justify-content: center;
		
		          .dot {
		              // width: 24rpx;
		              // height: 8rpx;
					  writing-mode : tb-rl;
					  letter-spacing: 20rpx;
					  font-size: 48rpx;
		              transition: all .6s;
		              color: rgba(0, 0, 0, .3);
		              margin-right: 10rpx;
		          }
		
		          .active {
		              // width: 24rpx;
		              // height: 8rpx;
					  font-size: 48rpx;
					  font-weight: bold;
		              color: rgba(255, 12, 39, 0.8);
		          }
		      }
	}

	.bg {
		height: 100vh;
		width: 100vh;
		
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	.selectButton {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 200rpx;
		height: 80rpx;
		line-height: 80rpx;
		position: absolute;
		bottom: 60rpx;
		right: 50rpx;
		border: 1rpx solid #FFFFFF;
		border-radius: 10rpx;
		background:rgba(0,0,0,0);
	}
	.selectButton text{
		font-weight: bold;
		color: #FFFFFF;
	}
	.switch {
		margin-right: 10rpx;
		width: 30rpx;
		height: 30rpx;
	}
	.popup-section {
		
		height: 400rpx;
	}
	.popup-title {
		margin: 20rpx 0 50rpx 0;
		display: inline-block;
		width: 100%;
		font-weight: bold;
		text-align: center;
	}
	.popup-content {
		display: flex;
		flex-wrap: wrap;
		/* justify-content: space-between; */
		padding: 0 40rpx;
		/* min-height: 400rpx; */
		.isActive {
			border: 1rpx solid #007AFF;
			text {
				color: #007AFF;
			}
		}
	}
	.radio-item {
		display: flex;
		margin-bottom: 40rpx;
		margin-right: 20rpx;
		width: 200rpx;
		height: 80rpx;
		border: 1rpx solid #3F536E;
	}
	.radio-item:nth-child(3n) {
		margin-right: 0;
	}
	.radio-item > text {
		width: 100%;
		text-align: center;
		line-height: 80rpx;
	}
	.popup-bottom {
		position: absolute;
		display: flex;
		border-top: 1rpx solid #dedede;
		bottom: 0;
		width: 100%;
		height: 100rpx;
	}
	.bottom-button {
		width: 50%;
		height: 100rpx;
		line-height: 100rpx;
		text-align: center;
	}
	.set-line {
		border-right: 1rpx solid #dedede;
	}
	.set-color {
		color: #007AFF;
	}
	.set-bottom {
		height: 100rpx;
	}
	.swiper {
		width: 100%;
		height: 100vh;
		.swiper-item{
			width: 100%;
			height: 100%;
		}

	}
	.type-desc {
		position: absolute;
		top: 140rpx;
		left: 60rpx;
		color: white;
	}
	.type-desc
	view:nth-child(1) { 
		font-weight: bold;
		font-size: 62rpx;
	}
	view:nth-child(2) { 
		font-size: 32rpx;
	}
	view:nth-child(3) { 
		font-size: 32rpx;
	}
	view:nth-child(4) { 
		font-size: 32rpx;
	}
	
</style>

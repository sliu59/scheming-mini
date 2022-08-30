<template>
	<view>

				<uni-section title="基本用法" type="line">
					<view class="example">
						<!-- 基础用法，不包含校验规则 -->
						<uni-forms ref="baseForm" :modelValue="baseFormData">
							<uni-forms-item label="城市" required @click="citySelect">
								<uni-easyinput @click="citySelect" v-model="baseFormData.name" placeholder="请选择城市" />
							</uni-forms-item>
							<uni-forms-item label="户型面积" required>
								<uni-easyinput v-model="baseFormData.name" placeholder="请输入房屋面积 单位:平方" />
							</uni-forms-item>
							<uni-forms-item label="厅数" required>
								<uni-number-box @change="changeValue" />
							</uni-forms-item>
							<uni-forms-item label="房间数" required>
								<uni-number-box @change="changeValue" />
							</uni-forms-item>
							<uni-forms-item label="厨房数" required>
								<uni-number-box @change="changeValue" />
							</uni-forms-item>
							<uni-forms-item label="卫生间数" required>
								<uni-number-box @change="changeValue" />
							</uni-forms-item>
							<uni-forms-item label="阳台数" required>
								<uni-number-box @change="changeValue" />
							</uni-forms-item>
							<uni-forms-item label="硬装设施" required>
								 <hpy-form-select :dataList="hobbyList" text="text" name="value" v-model="formData.hobbySelect" @change="change" />
							</uni-forms-item>
							<uni-forms-item label="补充" required>
								 <hpy-form-select :dataList="hobbys" text="text" name="value" v-model="formData.hobbySelect" @change="change" />
							</uni-forms-item>
							<uni-forms-item label="电话" required>
								<uni-easyinput v-model="baseFormData.name" placeholder="请输入电话号码" />
							</uni-forms-item>
							<uni-forms-item label="备注">
								<uni-easyinput type="textarea" v-model="baseFormData.introduction" placeholder="备注" />
							</uni-forms-item>
							
						</uni-forms>
					</view>
					
				</uni-section> 
				<uni-card title="产品包描述">
					<text>该产品包适合40~60m²的空间使用，空间较小，活泼的颜色能够让空间显得更加轻盈。</text>
				</uni-card>
				<uni-card title="产品包服务">
					<text>后续客户提供平面图或上门量房复尺，进一步确定该产品包是否符合空间使用，专属设计师跟进服务，直至家具摆放满意。</text>
				</uni-card>
				<uni-card title="产品包品质">
					<text>确保每个家具到达您家之前都是经过品质检验的，基础硬装完整，保证下单10天内拎包入住。</text>
				</uni-card>
				<view class="btn-box">
					<button class="uni-button submit-btn"  type="Primary" @click="submit">确认下单</button>
				</view>
	<city-select 
	@cityClick="cityClick"
	:formatName="formatName"
	:activeCity="activeCity"
	:obtainCitys="obtainCitys"
	>
	</city-select>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				formatName: 'title',
				activeCity:{id:1,title:'广州'},
				//显示的城市数据
				obtainCitys: [
					{
						id: 0,
						title: '南京'
					},
					{
						id: 1,
						title: '北京'
					},
					{
						id: 2,
						title: '天津'
					},
					{
						id: 3,
						title: '西安'
					},
					{
						id: 4,
						title: '广州'
					},
					{
						id: 5,
						title: '佛山'
					},
					{
						id: 6,
						title: '东莞'
					},
					{
						id: 7,
						title: '肇庆'
					},
					{
						id: 8,
						title: '深圳'
					},
					{
						id: 9,
						title: '梅州'
					},
					{
						id: 10,
						title: '湛江'
					},
					{
						id: 10,
						title: '云浮'
					}
				],
				formData:{
						hobbySelect:''
					},
					hobbyList: [{
						text: '足球',
						value: 1
					}, {
						text: '篮球',
						value: 2
					}, {
						text: '游泳',
						value: 3
					}],
				// 基础表单数据
				baseFormData: {
					name: '',
					age: '',
					introduction: '',
					sex: 2,
					hobby: [5],
					datetimesingle: 1627529992399
				},

				// 单选数据源
				sexs: [{
					text: '男',
					value: 0
				}, {
					text: '女',
					value: 1
				}, {
					text: '保密',
					value: 2
				}],
				// 多选数据源
				hobbys: [{
					text: '需要设计师优化',
					value: 0
				}, {
					text: '不需要，已有设计师团队',
					value: 1
				},],
				// 分段器数据
				current: 0,
	
				// 校验表单数据
				valiFormData: {
					name: '',
					age: '',
					introduction: '',
				},
				// 校验规则
				rules: {
					name: {
						rules: [{
							required: true,
							errorMessage: '姓名不能为空'
						}]
					},
					age: {
						rules: [{
							required: true,
							errorMessage: '年龄不能为空'
						}, {
							format: 'number',
							errorMessage: '年龄只能输入数字'
						}]
					}
				},
				// 自定义表单数据
				customFormData: {
					name: '',
					age: '',
					hobby: []
				},
				// 自定义表单校验规则
				customRules: {
					name: {
						rules: [{
							required: true,
							errorMessage: '姓名不能为空'
						}]
					},
					age: {
						rules: [{
							required: true,
							errorMessage: '年龄不能为空'
						}]
					},
					hobby: {
						rules: [{
								format: 'array'
							},
							{
								validateFunction: function(rule, value, data, callback) {
									if (value.length < 2) {
										callback('请至少勾选两个兴趣爱好')
									}
									return true
								}
							}
						]
					}

				},
	
			}
		},
		computed: {
			// 处理表单排列切换
		},
		onLoad() {},
		onReady() {
			// 设置自定义表单校验规则，必须在节点渲染完毕后执行
			this.$refs.baseForm.setRules(this.customRules)
		},
		methods: {
			radioChange: function(evt) {
			            for (let i = 0; i < this.hobbys.length; i++) {
			                if (this.hobbys[i].value === evt.detail.value) {
			                    this.current = i;
			                    break;
			                }
			            }
			        },
				changeValue(value) {
							console.log('返回数值：', value);
						},
			onClickItem(e) {
				console.log(e);
				this.current = e.currentIndex
			},
			add() {
				this.dynamicLists.push({
					label: '域名',
					rules: [{
						'required': true,
						errorMessage: '域名项必填'
					}],
					id: Date.now()
				})
			},

			submit(ref) {
				this.$refs[ref].validate().then(res => {
					console.log('success', res);
					uni.showToast({
						title: `校验通过`
					})
				}).catch(err => {
					console.log('err', err);
				})
			},
			citySelect() {
				console.log(123);
			},
			cityClick(item) {
				console.log(2);
				uni.showToast({
					icon: 'none',
					title: 'item: ' + JSON.stringify(item),
					// #ifdef MP-WEIXIN
					duration: 3000,
					// #endif
					mask: true
				})
			}
		}
	}
</script>

<style lang="less">
.example {
		padding: 15px;
		background-color: #fff;
	}

	.segmented-control {
		margin-bottom: 15px;
	}

	.button-group {
		margin-top: 15px;
		display: flex;
		justify-content: space-around;
	}

	.form-item {
		display: flex;
		align-items: center;
	}

	.button {
		display: flex;
		align-items: center;
		height: 35px;
		margin-left: 10px;
	}
	.btn-box {
		padding-bottom: 40px;
		
	}
	.submit-btn {
		margin: 0 40px;
		
	}
</style>

<template>
	<view class="button-sp-area">
		<button type="primary" plain="true" @click="handelIdCardFront()">身份证正面</button>
		<button type="primary" plain="true" @click="handelIdCardBack()">身份证反面</button>
		<button type="primary" plain="true" @click="handelIdCardFrontLocal()">身份证正面(本地)</button>
		<button type="primary" plain="true" @click="handelIdCardBackLocal()">身份证反面(本地)</button>
		<button type="primary" plain="true" @click="handelBusiness()">营业执照</button>
		<button type="primary" plain="true" @click="handelBankcard()">银行卡</button>
		<button type="primary" plain="true" @click="handelVehicle('front')">行驶证主页</button>
		<button type="primary" plain="true" @click="handelVehicle('back')">行驶证副页</button>
		<button type="primary" plain="true" @click="handelDriving()">驾驶证</button>
		<button type="primary" plain="true" @click="handelGeneralBasic()">通用文字识别(不含位置信息版)</button>
		<button type="primary" plain="true" @click="handelGeneral()">通用文字识别(含位置信息)</button>
		<button type="primary" plain="true" @click="handelGeneralEnchanced()">通用文字识别(含生僻字版)</button>
		<button type="primary" plain="true" @click="handelGeneralAccurate()" style="font-size: 14px;">通用文字识别(高精度，带位置信息)</button>
		<button type="primary" plain="true" @click="handelGeneralAccurateBasic()" style="font-size: 14px;">通用文字识别(高精度，不带位置信息)</button>
		<button type="primary" plain="true" @click="handelWebImage()">网图识别</button>
		<button type="primary" plain="true" @click="handelReceipt()">通用票据识别</button>
		<button type="primary" plain="true" @click="handelIOCR()">iOCR 通用版</button>
	</view>
</template>

<script>
	const ocr = uni.requireNativePlugin('ChuJC-Baidu-OCR');
	export default {
		data() {
			return {
				title: ''
			}
		},
		onLoad() {

		},
		methods: {
			handelIdCardFront() {
				ocr.idCardFront({
					detect_photo: 'true', // 百度文档中的参数选型 具体参考百度文档 https://ai.baidu.com/ai-doc/OCR/rk3h7xzck
					is_return_image: 'true' // 自定义参数 主要用于是否返回 识别的图片
				}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelIdCardBack() {
				ocr.idCardBack({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelIdCardFrontLocal() {
				ocr.idCardFrontLocal({
					detect_photo: 'true'
				}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelIdCardBackLocal() {
				ocr.idCardBackLocal({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelBusiness() {
				ocr.businessLicense({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelBankcard() {
				ocr.bankCard({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelVehicle(vehicle_license_side) {
				// 注意vehicle_license_side参数默认front  具体可以参考官方文档 https://ai.baidu.com/ai-doc/OCR/yk3h7y3ks
				let params = {}
				if(vehicle_license_side === 'back') {
					params.vehicle_license_side = vehicle_license_side
				}
				ocr.vehicleLicense(params, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelDriving() {
				ocr.drivingLicense({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelGeneral() {
				ocr.general({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelGeneralBasic() {
				ocr.generalBasic({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelGeneralEnchanced() {
				ocr.generalEnchanced({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelGeneralAccurate() {
				ocr.generalAccurate({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelGeneralAccurateBasic() {
				ocr.generalAccurateBasic({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelWebImage() {
				ocr.webImage({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelReceipt() {
				ocr.receipt({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			},
			handelIOCR() {
				ocr.iOCR({}, result => {
					const msg = JSON.stringify(result);
					uni.showModal({
						title: "返回信息",
						content: msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				});
			}
		}
	}
</script>

<style>
	.button-sp-area {
		margin: 0 auto;
		width: 90%;
	}
	.button-size {
		font-size: 14px;
	}
</style>

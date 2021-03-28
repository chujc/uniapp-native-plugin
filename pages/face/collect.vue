<template>
	<view class="button-sp-area">
		<button type="primary" plain="true" @click="handelFaceCollect(false)">人脸采集(包含动作活体)</button>
		<button type="primary" plain="true" @click="handelFaceCollect(true)">人脸采集(随机动作活体)</button>
		<button type="primary" plain="true" @click="handelFaceCollectFalse()">人脸采集(不包含动作活体)</button>
		<view v-show="status">
			<image class="code" :src="image" />
		</view>
	</view>
</template>

<script>
	const Face = uni.requireNativePlugin('ChuJC-Baidu-Face-Collect');
	export default {
		data() {
			return {
				title: "",
				status: false,
				image: "data:image/png;base64,",
				faceInitStatus: false
			}
		},
		onLoad() {

		},
		mounted() {
			this.initFaceSdk();
		},
		methods: {
			initFaceSdk() {
				Face.init({
					appName: "testplugin"
				}, result => {
					const msg = JSON.stringify(result);
					console.log(msg)
					if (result.code == 200) {
						this.faceInitStatus = true
					}
				})
			},
			handelFaceCollect(random) {
				if (!this.faceInitStatus) {
					uni.showModal({
						title: "SDK初始化失败",
						content: "请检查初始化参数、授权文件",
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
					return;
				}
				let livenessType = [ 'Eye', 'Mouth', 'HeadRight', 'HeadLeft', 'HeadUp', 'HeadDown' ];
				const randomNum = parseInt(Math.random()*(5)) + 2;
				let lelivenessTypeList = this.getRandomArrayElements(livenessType, randomNum);
				Face.collect({
					isActionLive: "true",
					isLivenessRandom: random ? "true" : "false",
					livenessTypeList: lelivenessTypeList
				}, result => {
					const msg = JSON.stringify(result);
					console.log(msg)
					uni.showModal({
						title: "返回信息",
						content: result.msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
					if(result.hasOwnProperty("image")) {
						this.status = true;
						this.image = "data:image/png;base64," + result.image;
					} 
				});
			},
			handelFaceCollectFalse() {
				if (!this.faceInitStatus) {
					uni.showModal({
						title: "SDK初始化失败",
						content: "请检查初始化参数、授权文件",
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
					return;
				}
				Face.collect({
					isActionLive: "false"
				}, result => {
					const msg = JSON.stringify(result);
					console.log(msg)
					uni.showModal({
						title: "返回信息",
						content: result.msg,
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
					if(result.hasOwnProperty("image")) {
						this.status = true;
						this.image = "data:image/png;base64," + result.image;
					} 
				});
			},
			getRandomArrayElements(arr, count) {
			    var shuffled = arr.slice(0), i = arr.length, min = i - count, temp, index;
			    while (i-- > min) {
			        index = Math.floor((i + 1) * Math.random());
			        temp = shuffled[index];
			        shuffled[index] = shuffled[i];
			        shuffled[i] = temp;
			    }
			    return shuffled.slice(min);
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
	.code {
		width: 100%;
		height: 640px;
	}
</style>

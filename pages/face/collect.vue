<template>
	<view class="button-sp-area">
		<button type="primary" plain="true" @click="handelFaceCollect()">人脸采集(包含动作活体)</button>
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
				image: "data:image/png;base64,"
			}
		},
		onLoad() {

		},
		methods: {
			handelFaceCollect(random) {
				let livenessType = [ 'Eye', 'Mouth', 'HeadRight', 'HeadLeft', 'HeadUp', 'HeadDown', 'HeadLeftOrRight' ];
				const randomNum = parseInt(Math.random()*(6)) + 2;
				let lelivenessTypeList = this.getRandomArrayElements(livenessType, randomNum);
				Face.collect({
					appName: "testplugin",
					isActionLive: "true",
					isLivenessRandom: "random",
					livenessTypeList: lelivenessTypeList
				}, result => {
					const msg = JSON.stringify(result);
					console.log(msg)
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
					if(result.hasOwnProperty("image")) {
						this.status = true;
						this.image = "data:image/png;base64," + result.image;
					} 
				});
			},
			handelFaceCollectFalse() {
				Face.collect({
					appName: "testplugin",
					isActionLive: "false"
				}, result => {
					const msg = JSON.stringify(result);
					console.log(msg)
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
					if(result.hasOwnProperty("image")) {
						this.status = true;
						this.image = "data:image/png;base64," + result.image;
					} 
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

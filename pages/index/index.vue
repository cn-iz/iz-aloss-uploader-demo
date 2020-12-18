<template>
	<view class="content">
		<button @tap="upload">上传</button>
		<view @click="ossPutProject">{{progress?'上传进度：'+progress:''}}</view>
	</view>
</template>

<script>
	import izUploader from '@/components/iz-aloss-uploader/iz-aloss-uploader.js'
	export default {
		data() {
			return {
				title: 'Hello',
				progress:0,
			}
		},
		onLoad() {

		},
		methods: {
			upload(){
				let that =this
				uni.chooseImage({
					success:function(res){
						let uploadTask = izUploader(res.tempFilePaths[0],'png',data=>{
							console.log(data)
						},err=>{
							console.log(err)
						})
						uploadTask.onProgressUpdate(async function(r) {
							console.log(r)
							that.progress = r.progress
						});
					}
				})
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>

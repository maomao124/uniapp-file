<template>
	<view>
		<button type="primary" @click="button1">选择文件保存</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {
			button1() {
				uni.chooseImage({
					success: function(res) {
						var tempFilePaths = res.tempFilePaths;
						uni.saveFile({
							tempFilePath: tempFilePaths[0],
							success: function(res) {
								var savedFilePath = res.savedFilePath;
								console.log("保存文件路径：",savedFilePath);
							},
							fail: (err) => {
								console.log("文件保存失败：",err);
							}
						});
					}
				});
			}
		}
	}
</script>

<style>

</style>
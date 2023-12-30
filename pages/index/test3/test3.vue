<template>
	<view>
		<button type="primary" @click="button1">选择文件保存</button>
		<button type="primary" @click="button2">查看已保存的文件</button>
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
			},
			button2() {
				uni.getSavedFileList({
					success: (data) => {
						console.log(data.fileList);
					},
					fail: (err) => {
						console.log("获取文件列表失败：",err);
					}
				})
			}
		}
	}
</script>

<style>
button{
	margin: 5px;
}
</style>
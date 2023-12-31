<template>
	<view>
		<button type="primary" @click="button1">选择文件保存</button>
		<button type="primary" @click="button2">查看已保存的文件</button>
		<text>文件列表：</text>
		<view v-for="file in fileList" :key="file.filePath">
			<button type="warn" @click="button3(file.filePath)">{{file.filePath}}</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fileList:[],
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
						this.fileList=data.fileList;
					},
					fail: (err) => {
						console.log("获取文件列表失败：",err);
					}
				})
			},
			button3(path)
			{
				console.log(path);
				uni.getSavedFileInfo({
					filePath:path,
					success: (data) => {
						console.log(data);
						uni.showModal({
							showCancel:false,
							title:'文件信息',
							content:'文件信息：'+JSON.stringify(data)
						})
					},
					fail(err) {
						console.log(err);
						uni.showModal({
							title:'错误',
							content:'查看文件信息失败!'
						})
					}
				})
			}
		},
		onShow() {
			uni.getSavedFileList({
				success: (data) => {
					console.log(data.fileList);
					this.fileList=data.fileList;
				},
				fail: (err) => {
					uni.showModal({
						title:'错误',
						content:'读取文件列表失败!'
					})
				}
			})
		}
	}
</script>

<style>
button{
	margin: 5px;
}
text{
	color: coral;
	font-size: 1.5em;
}
</style>
<template>
	<view>
		<button type="primary" @click="openPdf2()">打开pdf文件</button>
		<button type="primary" @click="openDocx()">打开docx文件</button>
		<button type="primary" @click="openXlsx()">打开xlsx文件</button>
		<button type="primary" @click="openPpt()">打开ppt文件</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				baseUrl:'http://localhost:8080/',
			}
		},
		methods: {
			openPdf()
			{
				uni.showLoading({})
				uni.downloadFile({
					url: this.baseUrl+ '/static/pdf',
					//url: 'https://example.com/somefile.pdf',
					success: (data) => {
						uni.hideLoading();
						console.log("打开pdf");
						var filePath = data.tempFilePath;
						uni.openDocument({
							filePath: filePath,
							fileType:'pdf',
							showMenu: true,
							success: (res) => {
								console.log("打开成功");
							},
							fail: (err) => {
								console.log(err);
								uni.showModal({
									title:'提示',
									content:'文件打开失败',
									showCancel:false
								})
							}
						})
					},
					fail: (err) => {
						uni.hideLoading();
						console.log(err);
						uni.showModal({
							title:'提示',
							content:'文件下载失败',
							showCancel:false
						})
					}
				})
				
			},
			openPdf2()
			{
				uni.showLoading({})
				uni.downloadFile({
					url: this.baseUrl+ '/static/pdf',
					//url: 'https://example.com/somefile.pdf',
					success: (data) => {
						uni.saveFile({
							tempFilePath:data.tempFilePath,
							success: (res) => {
								uni.hideLoading();
								console.log("打开pdf");
								var filePath = res.savedFilePath;
								uni.openDocument({
									filePath: filePath,
									fileType:'pdf',
									showMenu: true,
									success: (res) => {
										console.log("打开成功");
									},
									fail: (err) => {
										console.log(err);
										uni.showModal({
											title:'提示',
											content:'文件打开失败',
											showCancel:false
										})
									}
								})
							},
							fail: (err) => {
								uni.hideLoading();
								uni.showModal({
									title:'提示',
									content:'文件保存失败',
									showCancel:false
								})
							}
						})
					},
					fail: (err) => {
						uni.hideLoading();
						console.log(err);
						uni.showModal({
							title:'提示',
							content:'文件下载失败',
							showCancel:false
						})
					}
				})
			},
			openDocx()
			{
				uni.showLoading({})
				uni.downloadFile({
					url: this.baseUrl+ '/static/docx',
					success: (data) => {
						uni.hideLoading();
						console.log("打开docx");
						uni.openDocument({
							filePath: data.tempFilePath,
							fileType:'docx',
							showMenu: true,
							success: (res) => {
								console.log("打开成功");
							},
							fail: (err) => {
								console.log(err);
								uni.showModal({
									title:'提示',
									content:'文件打开失败',
									showCancel:false
								})
							}
						})
					},
					fail: (err) => {
						uni.hideLoading();
						console.log(err);
						uni.showModal({
							title:'提示',
							content:'文件下载失败',
							showCancel:false
						})
					}
				})
				
			},
			openXlsx()
			{
				uni.showLoading({})
				uni.downloadFile({
					url: this.baseUrl+ '/static/xlsx',
					success: (data) => {
						uni.hideLoading();
						console.log("打开xlsx");
						uni.openDocument({
							filePath: data.tempFilePath,
							fileType:'xlsx',
							showMenu: true,
							success: (res) => {
								console.log("打开成功");
							},
							fail: (err) => {
								console.log(err);
								uni.showModal({
									title:'提示',
									content:'文件打开失败',
									showCancel:false
								})
							}
						})
					},
					fail: (err) => {
						uni.hideLoading();
						console.log(err);
						uni.showModal({
							title:'提示',
							content:'文件下载失败',
							showCancel:false
						})
					}
				})
				
			},
			openPpt()
			{
				uni.showLoading({})
				uni.downloadFile({
					url: this.baseUrl+ '/static/ppt',
					success: (data) => {
						uni.hideLoading();
						console.log("打开ppt");
						uni.openDocument({
							filePath: data.tempFilePath,
							fileType:'ppt',
							showMenu: true,
							success: (res) => {
								console.log("打开成功");
							},
							fail: (err) => {
								console.log(err);
								uni.showModal({
									title:'提示',
									content:'文件打开失败',
									showCancel:false
								})
							}
						})
					},
					fail: (err) => {
						uni.hideLoading();
						console.log(err);
						uni.showModal({
							title:'提示',
							content:'文件下载失败',
							showCancel:false
						})
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

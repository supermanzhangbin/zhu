<template>
	<view class="content">
		<view class="title">
			{{title}}...
		</view>
		<view class="art-content">
			<!-- nodes支持数组和字符串的类型,主要是渲染html格式的 -->
			<rich-text class="richText" :nodes="strings">
			</rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title : '',
				strings : ''
			};
		},
		onLoad(e) {
			uni.showLoading({
				title: '加载中...',
			});
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					uni.hideLoading();
					console.log('请求的数据为',res);
					this.title = res.data.title;
					this.strings = res.data.content;
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.content {
	padding: 10upx 2%;
	width: 96%;
	flex-wrap: wrap; /* 允许换行 */
}
.title {
	line-height: 2em;
	font-weight: 700;
	font-size: 38upx;
}
</style>

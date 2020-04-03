<template>
	<view class="content">
		<news-list :list="list" v-if="list.length"></news-list>
	</view>
</template>

<script>
	import NewsList from '../../../components/NewsList.vue'
	export default {
		components: {
			NewsList
		},
		data() {
			return {
				list: []
			};
		},
		onLoad() {
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					this.list = res.data
				},
				fail: () => {},
				complete: () => {}
			});

		},
	}
</script>

<style lang="scss">
	.content {
		padding: 32rpx;
	}

</style>

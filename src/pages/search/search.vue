<template>
	<view>
		<search-comp></search-comp>
		<source-list :list="list" v-if="list.length"></source-list>
	
	</view>
</template>

<script>
	import SearchComp from '../../components/Search.vue'
	import SourceList from '../../components/SourceList.vue'
	export default {
		components: {
			SearchComp,
			SourceList
		},
		data() {
			return {
				list: []
			}
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

		methods: {

		}
	}
</script>

<style lang="scss">
</style>

<template name="Search">
	<view class="cu-bar bg-white search">
		<view class="search-form radius">
			<text class="cuIcon-search"></text>
			<input @focus="InputFocus" @blur="InputBlur" :adjust-position="false" type="text" placeholder="搜索图片、文章、视频"
			 confirm-type="search"></input>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'Search',
		data() {
			return {

			};
		},
		methods: {
		      InputFocus(e) {
		        this.InputBottom = e.detail.height
		      },
		      InputBlur(e) {
		        this.InputBottom = 0
		      }
		    }
	}
</script>

<style lang="scss">
	.cu-bar .search-form {
		height: 70rpx;
		line-height: 70rpx;
		margin: 0 32rpx;
	}

</style>

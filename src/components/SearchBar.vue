<template name="SearchBar">
	<view class="box">
		<view class="cu-bar search">
			<navigator class="action border-r-b" url="/pages/citys/citys">
				<text class="margin-right-xs">郑州</text>
				<text class="cuIcon-triangledownfill"></text>
			</navigator>
			<navigator url="/pages/search/search" class="search-form round">
				<text class="cuIcon-search"></text>
				<input class="text-left" @focus="InputFocus" @blur="InputBlur" :adjust-position="false" type="text" placeholder="大家都在搜: 华科-滨河府"
				 confirm-type="search"></input>
			</navigator>

		</view>
	</view>
</template>

<script>
	export default {
		name: 'SearchBar',
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
	.box {
		height: 70rpx;
		margin: 0 32rpx;
		background-color: #F7F7F7;

		.border-r-b {
			position: relative;

			&::after {
				content: "";
				width: 2rpx;
				height: 40rpx;
				background: rgba(216, 216, 216, 1);
			}
		}

		.cu-bar {
			min-height: 70rpx;

			.search-form {
				margin: 0;
			}
		}

	}
</style>

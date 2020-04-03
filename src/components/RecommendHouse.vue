<template name="RecommendHouse">
	<view class="overflow-auto-x">
		<view class="list-box flex">
			<view class="list-item" v-for="(item,index) in list" :key="index">
				<view class="address flex align-center">
					<image class="icon black" src="../static/images/location-icon.png"></image>
					<text class="address-text black">河南省郑州市郑东新区天则街201号</text>
				</view>
				<view class="flex">
					<image class="img radius" :src="item.author_avatar"></image>
					<view class="flex-sub">
						<view class="title">{{item.title}}</view>
						<view class="text-desc text-black">
							{{item.summary}}
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
	</template>

<script>
	export default {
		name: 'RecommendHouse',
		props: {
			list: {
				type: Array,
				default(){
					return []
				}
			}
		},
		data() {
			return {
				
			};
		},
		mounted() {
			
		}
	}
</script>

<style lang="scss">
	.list-box {
		.list-item{
			width: 650rpx;
			margin-bottom: 32rpx;
		}
		.icon{
			width: 40rpx;
			height: 48rpx;
			margin-right: 28rpx;
		}
		.address{
			margin-bottom: 28rpx;
		}
		.address-text {
			font-size:28rpx;
			color:rgba(170,170,170,1);
		}
		.img {
			width: 456rpx;
			height: 286rpx;
			margin-right: 20rpx;
			object-fit: cover;
		}

		.title {
			font-size:44rpx;
			font-weight:bold;
			color:rgba(56,68,127,1);
		}

		.text-desc {
			font-size:28rpx;
			color:rgba(153,153,153,1);
		}
	}
</style>


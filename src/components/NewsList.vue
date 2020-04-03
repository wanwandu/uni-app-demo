<template name="NewsList">
	<view class="list-box">
		<view class="list-item flex" v-for="(item,index) in list" :key="index" @click="goDetail(item)">
			<image class="img radius" :src="item.author_avatar"></image>
			<view class="flex-sub">
				<view class="title compulsory-row-one">{{item.title}}</view>
				<view class="text-desc compulsory-row-two">
					{{item.summary}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'NewsList',
		props: {
			list: {
				type: Array,
				default () {
					return []
				}
			},
			aa: {
				type: String,
				default: ''
			}
		},
		data() {
			return {
			};
		},
		mounted() {
		},
		methods: {
			goDetail(item) {
				console.log(item)
				uni.navigateTo({
					url: '../../pages/hot/hot?item=' + item
				});
			}
		}
	}
</script>

<style lang="scss">
	.list-box {
		.list-item {
			margin-bottom: 32rpx;
		}

		.img {
			width: 200rpx;
			height: 150rpx;
			margin-right: 16rpx;
			object-fit: cover;
		}

		.title {
			font-size: 28rpx;
			font-weight: 500;
			color: rgba(51, 51, 51, 1);
		}

		.text-desc {
			font-size: 24rpx;
			color: rgba(102, 102, 102, 1);
		}
	}
</style>

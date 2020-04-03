<template name="SourceList">
	<view class="list-box">
		<view class="list-item flex" v-for="(item,index) in list" :key="index" @click="goDetail(item)">
			<view class="img-box">
				<image class="img radius" :src="item.author_avatar"></image>
				<view class="img-zz text-xs text-white">10.1w人围观</view>
			</view>

			<view class="flex-sub">
				<view class="title compulsory-row-one">{{item.title}}</view>
				<view class="list-price padding-top-xs">
					<text>均价</text>
					<text class="price text-red text-price padding-lr-xs">80.00</text>
					<text>元</text>
				</view>
				<view class="address compulsory-row-one padding-top-xs"> 经开十七大街英文二路与金</view>
				<view class='flex flex-wrap'>
					<view class="padding-right-xs padding-tb-xs">
						<view class='cu-tag bg-tag-blue radius'>住宅</view>
					</view>
					<view class="padding-right-xs padding-tb-xs">
						<view class='cu-tag bg-tag-blue radius'>纯别墅区</view>
					</view>
				</view>
			</view>
			<view class="margin-left-sm">
				<i class="collection-icon collection-icon-default"></i>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'SourceList',
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
		methods:{
			goDetail(item){
				console.log(item.id)
				uni.navigateTo({
					url: '/pages/hot/hot?item=' + item.id,
				});
				
			}
		}
	}
</script>

<style lang="scss">
.list-box {
	padding: 10rpx 32rpx 0;
		.list-item {
			margin-bottom: 32rpx;
		}
		.img-box {
			position: relative;
			margin-right: 20rpx;
		}
		.img-zz {
			width: 100%;
			height: 44rpx;
			line-height: 44rpx;
			background:rgba(0, 0, 0, .5) url(~@/static/images/see-icon.png) 16rpx 10rpx no-repeat;
			background-size: 24rpx 24rpx;
			padding-left:56rpx;
			position: absolute;
			left: 0;
			bottom: 0;
			
		}

		.img {
			width: 280rpx;
			height: 210rpx;
			object-fit: cover;
		}

		.title {
			font-size: 30rpx;
			font-weight: 500;
			color: rgba(51, 51, 51, 1);
		}

		.list-price {
			font-size: 28rpx;
			color: rgba(51, 51, 51, 1);
		}

		.price {
			font-size: 44rpx;
			font-weight: bold;
			color: rgba(243, 72, 71, 1);
		}

		.address {
			font-size: 24rpx;
			color: rgba(153, 153, 153, 1);
		}
	}

</style>

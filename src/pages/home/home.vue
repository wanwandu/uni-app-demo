<template>
	<view class="padding-top-xs">
		<search-bar></search-bar>
		<!-- banner -->
		<view class="banner">
			<swiper class="screen-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
			 :autoplay="true" interval="5000" duration="500">
				<swiper-item v-for="(item,index) in swiperList" :key="index">
					<image class="radius" :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
					<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
				</swiper-item>
			</swiper>
		</view>
		<!-- 金刚区 -->
		<view class="flex cell-box justify-around">
			<view class="text-center" v-for=" (item, index) in cellList" :key="index">
				<image class="block img" :src="item.icon"></image>
				<text class="text">{{item.name}}</text>
			</view>
		</view>
		<!-- 好盘推荐 -->
		<view class="group-box">
			<view class="flex justify-between align-end header">
				<view class="">
					<text class="title">好盘推荐</text>
				</view>
				<view class="more">更多></view>
			</view>
			<view>
				<view class="overflow-auto-x">
					<recommend-house :list="newslist" v-if="newslist.length"></recommend-house>
				</view>
			</view>


		</view>

		<view class="group-box">
			<view class="flex justify-between align-end header">
				<view>
					<text class="title">房产资讯</text>
				</view>
				<navigator url="../news/list/list">
					<view class="more">更多></view>
				</navigator>

			</view>
			<news-list :list="newslist" v-if="newslist.length"></news-list>


		</view>



	</view>
</template>

<script>
	import SearchBar from '../../components/SearchBar.vue'
	import NewsList from '../../components/NewsList.vue'
	import RecommendHouse from '../../components/RecommendHouse.vue'

	export default {
		components: {
			SearchBar,
			NewsList,
			RecommendHouse
		},
		data() {
			return {
				title: 'Hello',
				swiperList: [{
					id: 0,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big84000.jpg'
				}, {
					id: 1,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big37006.jpg',
				}, {
					id: 2,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big39000.jpg'
				}, {
					id: 3,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg'
				}, {
					id: 4,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big25011.jpg'
				}, {
					id: 5,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big21016.jpg'
				}, {
					id: 6,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big99008.jpg'
				}],
				dotStyle: false,
				towerStart: 0,
				direction: '',
				cellList: [{
					icon: require('../../static/images/housing-loan-train-icon.png'),
					name: '房贷直通车'
				}, {
					icon: require('../../static/images/housing-loan-icon.png.png'),
					name: '房贷计算'
				}, {
					icon: require('../../static/images/form-icon.png'),
					name: '活动报名'
				}, {
					icon: require('../../static/images/luck-draw-icon.png'),
					name: '在线抽奖'
				}],
				newslist: []
			}
		},
		onLoad(e) {
			console.log(e, 'aaaa')
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					console.log(res)
					this.newslist = res.data
					console.log(this.newslist, typeof(this.newslist), 'aaa--->')

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
	.banner {
		margin: 22rpx 32rpx 36rpx;

	}

	.cell-box {
		.img {
			width: 88rpx;
			height: 88rpx;
			margin: 0 auto 12rpx;
		}

		.text {
			font-size: 28rpx;
			color: rgba(51, 51, 51, 1);
		}
	}

	.group-box {
		margin: 48rpx 32rpx 0;

		.header {
			margin-bottom: 28rpx;
		}

		.title {
			font-size: 36rpx;
			font-weight: 600;
			color: rgba(51, 51, 51, 1);
		}

		.more {
			font-size: 20rpx;
			color: rgba(51, 51, 51, 1);
		}

	}
</style>

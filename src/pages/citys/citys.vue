<template>
	<view>
		<view class="bottom-borderu-bar bg-white search fixed" :style="[{top:CustomBar + 'px'}]">
			<search-comp></search-comp>
		</view>
		<view class="bottom-border align-center flex justify-between p-l-r">
			<view>
				<image class="location-icon" src="../../static/images/location-icon.png"></image>
				<text>郑州</text>
			</view>
			<view class="btn text-center">
				<text>重新定位</text>
			</view>
		</view>
		<view class="tags-box">
			<view class="tags-name">热门城市</view>
			<view class="flex flex-wrap">
				<view class="padding-xs">
					<view class='cu-tag bg-tag-city'>巩义</view>
				</view>
				<view class="padding-xs">
					<view class='cu-tag bg-tag-city'>新密</view>
				</view>
				<view class="padding-xs">
					<view class='cu-tag bg-tag-city'>荥阳</view>
				</view>
				<view class="padding-xs">
					<view class='cu-tag bg-tag-city'>上街</view>
				</view>
			</view>
		</view>
		<scroll-view scroll-y class="indexes" :scroll-into-view="'indexes-'+ listCurID" :style="[{height:'calc(100vh - '+ CustomBar + 'px - 50px)'}]"
		 :scroll-with-animation="true" :enable-back-to-top="true">
			<block v-for="(item,index) in list" :key="index">
				<view :class="'indexItem-' + item.name" :id="'indexes-' + item.name" :data-index="item.name">
					<view class="p-l-r margin-top-sm">{{item.name}}</view>
					<view class="cu-list menu-avatar no-padding">
						<view class="cu-item p-l-r" v-for="(items,sub) in 2" :key="sub">
							<view class="city-name" @tap="clickCity(list[sub].name)">{{item.name}}{{list[sub].name+'城市'}}</view>
						</view>
					</view>
				</view>
			</block>
		</scroll-view>
		<view class="indexBar" :style="[{height:'calc(100vh - ' + CustomBar + 'px - 50px)'}]">
			<view class="indexBar-box" @touchstart="tStart" @touchend="tEnd" @touchmove.stop="tMove">
				<view class="indexBar-item" v-for="(item,index) in list" :key="index" :id="index" @touchstart="getCur" @touchend="setCur">
					{{item.name}}</view>
			</view>
		</view>
		<!--选择显示-->
		<view v-show="!hidden" class="indexToast">
			{{listCur}}
		</view>

	</view>
</template>

<script>
	import SearchComp from '../../components/Search.vue'
	export default {
		components: {
			SearchComp
		},
		data() {
			return {
				StatusBar: this.StatusBar,
				CustomBar: 0,
				hidden: true,
				listCurID: '',
				list: [],
				listCur: '',

			};
		},
		onLoad() {
			let list = [{}];
			for (let i = 0; i < 26; i++) {
				list[i] = {};
				list[i].name = String.fromCharCode(65 + i);
			}
			this.list = list;
			this.listCur = list[0];
		},
		onReady() {
			let that = this;
			uni.createSelectorQuery().select('.indexBar-box').boundingClientRect(function(res) {
				that.boxTop = res.top
			}).exec();
			uni.createSelectorQuery().select('.indexes').boundingClientRect(function(res) {
				that.barTop = res.top
			}).exec()
			console.log(that.boxTop, 'that.boxTop')
			console.log(that.barTop, 'that.barTop')
		},
		methods: {
			//获取文字信息
			getCur(e) {
				this.hidden = false;
				this.listCur = this.list[e.target.id].name;
			},
			setCur(e) {
				this.hidden = true;
				this.listCur = this.listCur
			},
			//滑动选择Item
			tMove(e) {
				let y = e.touches[0].clientY,
					offsettop = this.boxTop,
					that = this;
				//判断选择区域,只有在选择区才会生效
				if (y > offsettop) {
					let num = parseInt((y - offsettop) / 20);
					this.listCur = that.list[num].name
				};
			},

			//触发全部开始选择
			tStart() {
				this.hidden = false
			},

			//触发结束选择
			tEnd() {
				this.hidden = true;
				this.listCurID = this.listCur
			},
			indexSelect(e) {
				let that = this;
				let barHeight = this.barHeight;
				let list = this.list;
				let scrollY = Math.ceil(list.length * e.detail.y / barHeight);
				for (let i = 0; i < list.length; i++) {
					if (scrollY < i + 1) {
						that.listCur = list[i].name;
						that.movableY = i * 20
						return false
					}
				}
			},
			clickCity(e) {
				console.log(e)
				uni.switchTab({
					url: '/pages/home/home?city=' + e
				})
			}
		}
	}
</script>

<style lang="scss">
	.location-icon {
		width: 28rpx;
		height: 32rpx;
		margin-right: 16rpx;
		vertical-align: sub;
	}

	.btn {
		width: 138rpx;
		height: 48rpx;
		line-height: 46rpx;
		font-size: 24rpx;
		color: rgba(56, 68, 127, 1);
		border-radius: 24rpx;
		margin: 30rpx 0;
		border: 2rpx solid rgba(75, 86, 139, 1);
	}
	.tags-box {
		margin: 56rpx 82rpx 0 32rpx;
	}

	.tags-name {
		font-size: 26rpx;
		color: rgba(153, 153, 153, 1);
	}

	.bg-tag-city {
		height: 64rpx;
		font-size: 26rpx;
		color: rgba(51, 51, 51, 1);
		background: rgba(248, 248, 248, 1);
		border-radius: 4rpx;
		padding: 0 40rpx;
		margin-top: 32rpx;
	}
	.city-name {
		font-size:30rpx;
		color:rgba(51,51,51,1);
	}

	.indexes {
		position: relative;
		margin-top: 80rpx;
	}

	.indexBar {
		position: fixed;
		right: 0px;
		bottom: 0px;
		padding: 20upx 20upx 20upx 60upx;
		display: flex;
		align-items: center;
	}

	.indexBar .indexBar-box {
		width: 40upx;
		height: auto;
		background: #fff;
		display: flex;
		flex-direction: column;
		box-shadow: 0 0 20upx rgba(0, 0, 0, 0.1);
		border-radius: 10upx;
	}

	.indexBar-item {
		flex: 1;
		width: 40upx;
		height: 40upx;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 24upx;
		color: #888;
	}

	movable-view.indexBar-item {
		width: 40upx;
		height: 40upx;
		z-index: 9;
		position: relative;
	}

	movable-view.indexBar-item::before {
		content: "";
		display: block;
		position: absolute;
		left: 0;
		top: 10upx;
		height: 20upx;
		width: 4upx;
		background-color: #f37b1d;
	}

	.indexToast {
		position: fixed;
		top: 0;
		right: 80upx;
		bottom: 0;
		background: rgba(0, 0, 0, 0.5);
		width: 100upx;
		height: 100upx;
		border-radius: 10upx;
		margin: auto;
		color: #fff;
		line-height: 100upx;
		text-align: center;
		font-size: 48upx;
	}
	.cu-list.menu-avatar>.cu-item {
		justify-content: initial;
		height: 88rpx;
	}
</style>

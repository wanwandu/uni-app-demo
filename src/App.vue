<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import "colorui/main.css";
	@import "colorui/icon.css";
	@import "common/common.css";
	page {
		width: 100%;
		min-height: 100%;
		background-color: #FFFFFF;
		
	}
	.compulsory-row-two {
		text-overflow: -o-ellipsis-lastline;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
	}
	
	.compulsory-row-one {
		text-overflow: -o-ellipsis-lastline;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 1;
		-webkit-box-orient: vertical;
	}
	.overflow-auto-x{
	    overflow-x: auto;
	    -webkit-overflow-scrolling: touch
	}
	.collection-icon {
		width: 32rpx;
		height: 32rpx;
		display: block;
		&-default {
			background: url(~@/static/images/collection-default.png);
			background-size: 100% 100%;
		}
		&-elected {
			background: url(~@/static/images/collection-selected.png);
			background-size: 100% 100%;
		}
		
	}
	.bg-tag-blue {
		font-size: 22rpx;
		padding: 0rpx 12rpx;
		height: 40rpx;
		background: rgba(220, 234, 255, 1);
		color: rgba(125, 166, 250, 1);
	}
	.p-l-r {
		padding: 0 32rpx;
	}
	.bottom-border{
		border: 2rpx solid #F4F4F4;
	}
	
	
	
</style>

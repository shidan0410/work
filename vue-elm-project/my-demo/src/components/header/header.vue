<script>
	import star from "components/star/star"

	export default {
		props:{
			seller: {
				type:Object
			}
		},
		data() {
			return {
				detailShow: false
			}
		},
		methods: {
			hideDetail() {
				this.detailShow = !this.detailShow
			}
		},
		created() {
			this.classMap = ['decrease','discount','special', 'invoice', 'guarantee']
		},
		components:{
			star
		}
	};

</script>

<template>
	<div class="header">
		<div class="content-wrapper">
			<div class="avatar">
				<img width="64" height="64" :src="seller.avatar" >
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="des">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div v-if="seller.supports" class="supports">
						<span class="icon" :class="classMap[seller.supports[0].type]"></span>
						<span class="text">{{seller.supports[0].description}}</span>
				</div>
			</div>
			<div class="support-count" v-if="seller.supports" @click="hideDetail">
				<span class="count">{{seller.supports.length}}个</span>
				<i class="icon-keyboard_arrow_right"></i>
			</div>
		</div>
		<div class="bulletin-wrapper" v-if="seller.bulletin" @click="hideDetail">
			<span class="bulletin-title"></span>
			<span class="bulletin-txt">{{seller.bulletin}}</span>
			<i class="icon-keyboard_arrow_right"></i>
		</div>
		<div class="detail" v-show="detailShow" transition="fade">
			<div class="detail-wapper">
				<div class="detail-main">
					<h1 class="name">{{seller.name}}</h1>
					<div class="star-wrapper">
						<star :size='48' :score="seller.score"></star>
					</div>
					<div class="title">
						<div class="line"></div>
						<div class="text">优惠信息</div>
						<div class="line"></div>
					</div>
					<ul class="supports" v-if="seller.supports">
						<li class="supports-item" v-for="item in seller.supports">
							<span class="icon" :class="classMap[seller.supports[0].type]" track-by="$index"></span>
							<span class="support-text">{{item.description}}</span>
						</li>
					</ul>
					<div class="title">
						<div class="line"></div>
						<div class="text">商家公告</div>
						<div class="line"></div>
					</div>
					<div class="bulletin">
						<p class="content">{{seller.bulletin}}</p>
					</div>
				</div>
			</div>
			<div class="detail-close" @click="hideDetail">
				<i class="icon-close">x</i>
			</div>
		</div>

	</div>
</template>

<style lang="stylus" rel="stylesheet/stylus">
	@import "../../common/stylus/index.styl"
	// @import "../../common/stylus/icon.styl"

	.header
		position relative
		background-color rgba(7, 17, 17, .5)
		overflow hidden
		.content-wrapper
			position relative
			padding-top 24px
			font-size 0
			.avatar
				display inline-block
				vertical-align top
				padding-left 24px
			.content
				display inline-block
				vertical-align top
				padding 2px 0 2px 16px
				.title
					.brand
						display inline-block
						vertical-align top
						width 30px
						height 18px
						bg-image('../../assets/brand')
						background-repeat no-repeat
						background-size 100%
					.name
						vertical-align top
						font-size 16px
						color rgb(255, 255, 255)
						font-weight bold
						line-height 18px
						margin-left 6px
				.des
					font-size 12px
					color rgb(255, 255, 255)
					font-weight 200
					line-height 12px
					margin 8px 0 10px 0
				.supports
					.text
						vertical-align middle
						font-size 10px
						color #fff
						margin-left 8px
					.icon
						display inline-block
						vertical-align middle
						width 12px
						height 12px
						background-size 12px 12px
						background-repeat no-repeat													
			.support-count
				position absolute
				right 12px
				bottom 0px
				padding 7px 8px
				background-color rgba(0, 0, 0, .2)
				border-radius 30px
				.count
					font-size 10px
					color #fff
					font-weight 200
					line-height 12px
		.bulletin-wrapper
				position relative
				margin-top 18px
				padding 0 16px 0 12px
				background-color rgba(7, 17, 27, .2)
				white-space nowrap
				text-overflow ellipsis
				overflow hidden
				.bulletin-title
					display inline-block
					vertical-align middle
					width 22px
					height 12px
					background-repeat no-repeat
					background-size 22px 12px
					bg-image('../../assets/bulletin')
				.bulletin-txt
					vertical-align middle
					font-size 10px
					margin-left 4px
					color rgb(255, 255, 255)
					font-weight 200
					line-height 28px
				.icon-keyboard_arrow_right
					position absolute
					right 12px
					top 12px
					font-size 10px
					color #fff						
		.detail
			position fixed
			width 100%
			height 100%
			top 0
			left 0
			color #fff
			font-size 0
			background-color rgba(7, 17, 27, .8)
			// filter blur(10px)
			// &.fade-transition
   //      opacity 0
   //      background rgba(7, 17, 27, 0.8)
   //    &.fade-enter, &.fade-leave
   //    	opacity 1
   //    	background rgba(7, 17, 27, 0)
			.detail-wapper
				height 100%
				min-height 100%
				.detail-main
					padding 64px 36px 32px 36px		
					.name
						text-align center
						font-size 16px
						font-weight 700
						line-height 32px
					.star-wrapper
						text-align center
						margin 16px 0 28px 0
					.title
						display flex
						.line
							position relative
							top -6px
							flex 1
							border-bottom 1px solid rgba(255, 255, 255, .2)
						.text
							padding 0 12px
							font-size 14px
							font-weight 500
					.supports
						font-size 12px
						font-weight 200
						line-height 24px
						margin 24px 0 28px 0
						.icon
							display inline-block
							vertical-align middle
							width 16px
							height 16px
							background-size 16px 16px
							margin-left 12px
						.support-text
							display inline-block
							vertical-align middle
							margin-left 6px
					.bulletin
						.content
							margin 24px 12px
							font-size 12px
							font-weight 200
							line-height 24px
			.detail-close
				margin -64px auto 0
				width 32px
				height 32px
				.icon-close
					width 32px
					height 32px
										
</style>

<script type="text/ecmascript-6">
	const LENGTH = 5
	const CLS_ON = "on"
	const CLS_HALF = "half"
	const CLS_OFF = "off"

	export default {
		props:{
			score:{
				type:Number
			},
			size:{
				type:Number
			}
		},
		computed: {
			starType() {
				return 'star-' + this.size
			},
			itemClasses() {
				let result = [];
				let score = Math.floor(this.score * 2) / 2;
				let hasHalf = score % 1 !==0
				let integer = Math.floor(score)

				for (let i = 0; i < integer; i++) {
					result.push(CLS_ON)
				}
				if(hasHalf){
					result.push(CLS_HALF)
				}
				if(result.length < LENGTH){
					result.push(CLS_OFF)
				}
				return result
			}
		}

	}

</script>


<template>
	<div class="star" :class="starType">
		<span class="star-item" v-for="item in itemClasses" :class="item"></span>
	</div>

</template>


<style type="text/stylus" lang="stylus">
	@import "../../common/stylus/index.styl"
	
	.star
		font-size 0
		.star-item
			display inline-block
		&.star-48
			.star-item
				width 20px
				height 20px
				background-size: 20px 20px
				margin-right 20px
				&.on
					bg-image("../../assets/star48_on")
				&.half
					bg-image("../../assets/star48_half")
				&.off
					bg-image("../../assets/star48_off")
		&.star-36
			.star-item
				width 15px
				height 15px
				background-size 15px 15px
				margin-right 15px
				&.on
					bg-image("../../assets/star36_on")
				&.half
					bg-image("../../assets/star36_half")
				&.off
					bg-image("../../assets/star36_off")
		&.star-24
			.star-item
				width 10px
				height 10px
				background-size 10px 10px
				margin-right 10px
				&.on
					bg-image("../../assets/star24_on")
				&.half
					bg-image("../../assets/star24_half")
				&.off
					bg-image("../../assets/star24_off")


</style>
<template>
	<div class="ratingselect">
		<div class="rating-type border-1px">
			<span @click="select(2,$event)" class="block positive" :class="{'active':type === 2}">{{desc.all}}<i class="count">{{ratings.length}}</i></span>
			<span @click="select(0,$event)" class="block positive" :class="{'active':type === 0}">{{desc.positive}}<i class="count">{{positives.length}}</i></span>
			<span @click="select(1,$event)" class="block negative" :class="{'active':type === 1}">{{desc.negative}}<i class="count">{{negatives.length}}</i></span>
		</div>
		<div @click="toggleContent" class="switch" :class="{'on':content}">
			<span class="icon-check_circle"></span>
			<span class="text">只看有内容的评价</span>
		</div>
	</div>
</template>
<script>
	const POSITIVE = 0
	const NEGATIVE = 1
	const ALL = 2
	export default {
		data() {
			return {
				type:2,
				content:false
			}
		},
		props: {
			ratings: {
				type:Array,
				default() {
					return []
				}
			},
			selectType: {
				type: Number,
				default : ALL
			},
			onlyContent: {
				type:Boolean,
				default:false
			},
			desc:{
				type:Object,
				default() {
					return {
						all:'全部',
						positive:'满意',
						negative:'不满意'
					}
				}
			}
		},
		methods: {
			select(type, event) {
				if (!event._constructed) {
                    return
                }
                this.type = type
                this.$emit('ratingTypeSelect', type)
			},
			toggleContent(event) {
				if (!event._constructed) {
                    return
                }
                this.content = !this.content
                this.$emit('content', this.content)
			}
		},
		computed: {
			positives() {
				return this.ratings.filter((rate) => {
					return rate.rateType === POSITIVE
				})
			},
			negatives() {
				return this.ratings.filter((rate) => {
					return rate.rateType === NEGATIVE
				})
			}
		}
	}
</script>
<style lang="stylus" rel="stylesheet/stylus">
	@import '../../common/stylus/mixin.styl' 
	.ratingselect
		.rating-type
			padding:18px 0
			margin:0 18px
			border-1px(rgba(7,17,27,0.1))
			font-size:0
			.block
				display:inline-block
				padding:8px 12px
				margin-right:8px
				line-height:16px
				border-radius:2px
				font-size:12px
				color:rgb(77,85,93)
				&.active
					color:#fff
				.count
					font-style:normal
					font-size:8px
					margin-left:2px
				&.positive
					background-color:rgba(0,160,220,0.2)
					&.active
						background-color:rgb(0,160,220)
				&.negative
					background-color:rgba(77,85,93,0.2)
					&.active
						background-color:rgb(77,85,93)
		.switch
			padding:12px 18px
			border-bottom:1px solid rgba(7,17,27,0.1)
			line-height:24px
			color:rgb(147,153,159)
			font-size:0
			&.on
				.icon-check_circle
					color:#00c850
			.icon-check_circle
				margin-right:4px
				font-size:24px
				display:inline-block
				vertical-align:top
			.text
				font-size:12px
				display:inline-block
				vertical-align:top
</style>
<template>
	<div class="cartcontrol">
		<transition name="move">
			<div class="cart-decrease" v-show="food.count" @click.stop.prevent="decreaseCart">
				<div class="inner icon-remove_circle_outline"></div>
			</div>
		</transition>
		<div class="cart-count" v-show="food.count">{{food.count}}</div>
		<div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
	</div>
</template>
<script>
	import Vue from 'vue'
	export default {
		props: {
			food: {
				type:Object
			}
		},
		methods: {
			addCart(event) {
				if (!event._constructed) {
                    return
                }
				if (!this.food.count) {
					Vue.set(this.food, 'count', 1)
				} else {
					this.food.count ++
				}
				this.$emit('add', event.target)
			},
			decreaseCart(event) {
				if (!event._constructed) {
                    return
                }
                if (this.food.count) {
                	this.food.count --
                }
			}
		}
	}
</script>
<style lang="stylus" rel="stylesheet/stylus">
	.cartcontrol
		font-size:0
		.cart-decrease
			display:inline-block
			padding:6px
			&.move-enter-active,&.move-leave-active
				transition:all 0.3s linear
			&.move-enter,&.move-leave-to
				opacity:0
				transform:translate3d(24px,0,0)
				.inner
					transform:rotate(180deg)
			.inner
				display:inline-block
				line-height:24px
				font-size:24px
				color:rgb(0,160,220)
				transition:all 0.3s linear
				transform:rotate(0)
		.cart-count
			display:inline-block
			vertical-align:top
			padding-top:6px
			width:12px
			line-height:24px
			text-align:center
			font-size:10px
			color:rgb(147,153,159)
		.cart-add
			display:inline-block
			padding:6px
			line-height:24px
			font-size:24px
			color:rgb(0,160,220)
</style>
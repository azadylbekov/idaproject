<template>
	<div @mouseover="isButtonShown = true" @mouseleave="isButtonShown = false" class="product-card">
		<img src="https://photobite.uk/wp-content/uploads/2021/04/polaroid-go-white.jpg" alt="">
		<div class="product-card-desc">
			<h3 class="product-card-desc__title">Наименование товара</h3>
			<p class="product-card-desc__para">Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк</p>
			<div class="product-card-desc__price">
				<span>10000 руб</span>
			</div>
		</div>
		<transition name="slide-up">
			<button v-show="this.isButtonShown" class="product-card__delete-btn"></button>
		</transition>
	</div>
</template>

<script>
	export default {
		name: "ProductCard",
		data() {
			return {
				isButtonShown: false,
			}
		},
		methods: {
		}
	}
</script>

<style lang="scss" scoped>
.product-card {
	background: #FFFEFB;
	box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
	border-radius: 4px;
	position: relative;
	height: 100%;
	img {
		width: 100%;
		border-radius: 4px 4px 0 0;
	}
	&-desc {
		padding: 16px 16px 24px 16px;
		text-align: left;
		&__title {
			font-weight: 600;
			margin: 0 0 16px 0;
			color: #3F3F3F;
			line-height: 25px;
			font-weight: 20px;
		}
		&__para {
			font-size: 16px;
			line-height: 20px;
			color: #3F3F3F;
		}
		&__price {
			margin-top: 32px;
			font-weight: 600;
			font-size: 24px;
			line-height: 30px;
		}
	}
	&__delete-btn {
		width: 32px;
		height: 32px;
		border-radius: 10px;
		background: #FF8484;
		box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
		position: absolute;
		border: 1px solid transparent;
		top: -10px;
		right: -10px;
		cursor: pointer;
		transition: 0.3s;
		&:after {
			content: '';
			background: url("../assets/delete.svg") no-repeat;
			width: 16px;
			height: 16px;
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
		}
		&:hover {
			transform: translateY(-5px);
			box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
		}
	}
}

.slide-up-enter-active, .slide-up-leave-active {
  transition: .3s;
}
.slide-up-enter, .slide-up-leave-to {
	transform: translateY(10px);
  opacity: 0;
}
</style>
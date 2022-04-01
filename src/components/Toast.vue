<template>
	<transition name="slide-down">
		<div v-show="isShown" class="toast">
			<div class="toast-content">
				Товар успешно добавлен!
			</div>
		</div>
	</transition>
</template>

<script>
	export default {
		name: "Toast",
		props: {
			isShown: {
				type: Boolean,
				default: true
			}
		}
	}
</script>

<style lang="scss" scoped>
.toast {
	position: fixed;
	top: 30px;
	left: 50%;
	background: #7BAE73;
	border-radius: 10px;
	color: #fff;
	transform: translate(-50%, 0);
	box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
	&-content {
		padding: 10px 20px;
	}
}

.slide-down-enter-active, .slide-down-leave-active {
  transition: .5s;
}
.slide-down-enter, .slide-down-leave-to {
	transform: translate(-50%, -80px);
  opacity: 0;
}
</style>
<template>
	<div class="filter-wrapper">
		<select class="filter-wrapper__select" id="cars" name="cars">
			<option value="default" selected>По умолчанию</option>
			<option value="min">По нарастающей</option>
			<option value="max">По убыванию</option>
			<option value="name">По наименованию</option>
		</select>
	</div>
</template>

<script>
	export default {
		name: "ProductFilter"
	}
</script>

<style lang="scss" scoped>
.filter-wrapper {
	display: flex;
	justify-content: flex-end;
	&__select {
		cursor: pointer;
		display: flex;
		justify-content: flex-end;
		box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
		border: 1px solid transparent;
		padding: 10px 5px 10px 5px;
		border-radius: 4px;
		outline: none;
		font-size: 12px;
		color: #B4B4B4;
		transition: 0.3s;
		&:focus {
			border-color: #3F3F3F; 
		}
	}
}
</style>
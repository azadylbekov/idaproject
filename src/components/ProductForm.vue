<template>
	<div class="product-form">
		<h2 class="product-form__title">Добавление товара</h2>
		<div class="product-form-card">
			<form class="product-form-block">
				<label class="product-form-block__req" for="name">
					<span>Наименование товара</span>
					<input id="name" type="text" placeholder="Введите наименование товара">
				</label>
				<label for="desc">
					<span>Описание товара</span>
					<textarea id="desc" placeholder="Введите описание товара"></textarea>
				</label>
				<label class="product-form-block__req" for="link">
					<span>Ссылка на изображение товара</span>
					<input id="link" type="text" placeholder="Введите ссылку">
				</label>
				<label class="product-form-block__req" for="price">
					<span>Цена товара</span>
					<input id="price" type="text" placeholder="Введите цену">
				</label>
				<button class="product-form-button product-form-button-disabled">Добавить товар</button>
			</form>
		</div>
	</div>
</template>

<script>
	export default {
		name: "ProductForm"
	}
</script>

<style lang="scss" scoped>
.product-form {
	&__title {
		font-size: 28px;
		line-height: 39px;
		font-weight: 600;
		color: #3F3F3F;
		margin: 0 0 16px 0;
		text-align: left;
	}
	&-card {
		background: #FFFEFB;
		box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
		border-radius: 4px;
		padding: 24px;
	}
	&-block {
		text-align: left;
		label	{
			color: #49485E;
		}
		&__req {
			span {
			position: relative;
				&:after {
					content: "";
					width: 4px;
					height: 4px;
					border-radius: 100%;
					background-color: #FF8484;
					position: absolute;
					top: 3px;
					right: -5px;
				}
			}
		}
	}
	input, textarea {
		color: #3F3F3F;
		font-weight: 400;
		font-size: 12px;
		line-height: 15px;
		border-radius: 4px;
		box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
		padding: 10px 0 10px 16px;
		outline: none;
		border: 1px solid transparent;
		width: 100%;
		margin-top: 4px;
		margin-bottom: 16px;
		box-sizing: border-box;
		transition: 0.3s;
		&::placeholder {
			color: #B4B4B4;
		}
		&:focus {
			border-color:#3F3F3F; 
		}
	}
	textarea {
		min-height: 108px;
		max-height: 150px;
		resize: vertical;
	}
	&-button {
		background: #7BAE73;
		border-radius: 10px;
		color: #fff;
		font-size: 12px;
		font-weight: 600;
		line-height: 15px;
		width: 100%;
		padding: 10px 0;
		border: none;
		box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
		cursor: pointer;
		&-disabled {
			background: #EEEEEE;
			box-shadow: none;
			color: #B4B4B4;
			cursor: unset;
		}
	}
}
</style>
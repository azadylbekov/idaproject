<template>
	<div class="product-form">
		<h2 class="product-form__title">Добавление товара</h2>
		<div class="product-form-card">
			<form @submit.prevent="submitForm" @change="this.checkValid" class="product-form-block">
				<label class="product-form-block__req" for="name">
					<span>Наименование товара</span>
					<input
						@input="checkValid"
						:class="`${!nameValid ? 'product-form-input-invalid' : ''}`" 
						v-model="name" 
						id="name" 
						type="text" 
						placeholder="Введите наименование товара">
					<p v-show="!nameValid" class="product-form-block__req-text">Поле является обязательным</p>
				</label>
				<label for="desc">
					<span>Описание товара</span>
					<textarea v-model="desc" id="desc" placeholder="Введите описание товара"></textarea>
				</label>
				<label class="product-form-block__req" for="link">
					<span>Ссылка на изображение товара</span>
					<input
						@input="checkValid" 
						:class="`${!linkValid ? 'product-form-input-invalid' : ''}`"  
						v-model="link" 
						id="link" 
						type="text" 
						placeholder="Введите ссылку">
					<p v-show="!linkValid" class="product-form-block__req-text">Поле является обязательным</p>
				</label>
				<label class="product-form-block__req" for="price">
					<span>Цена товара</span>
					<input
						@input="priceFormat"
						:class="`${!priceValid ? 'product-form-input-invalid' : ''}`"  
						v-model="price" 
						id="price" 
						placeholder="Введите цену"
						>
					<p v-show="!priceValid" class="product-form-block__req-text">Поле является обязательным</p>
				</label>
				<button 
					type="submit"
					:class="`product-form-button ${allValid ? '' : 'product-form-button-disabled'}`" 
					:disabled="!allValid">Добавить товар</button>
			</form>
		</div>
	</div>
</template>

<script>
	export default {
		name: "ProductForm",
		data() {
			return {
				name: "",
				desc: "",
				link: "",
				price: "",

				nameValid: true,
				linkValid: true,
				priceValid: true,
				allValid: false
			}
		},
		methods: {
			clearForm() {
				this.name = "";
				this.desc = "";
				this.link = "";
				this.price = "";
				this.nameValid = true;
				this.linkValid = true;
				this.priceValid = true;
				this.allValid = false;
			},
			submitForm() {
				let form = {
					name: this.name,
					desc: this.desc,
					link: this.link,
					price: this.price
				}
				this.$emit("submitForm", form);
				this.clearForm()
			},
			checkValid() {
				this.nameValid = this.name.length ? true : false;
				this.linkValid = this.link.length ? true : false;
				this.priceValid = this.price.length ? true : false;

				if(this.nameValid && this.linkValid && this.priceValid) {
					this.allValid = true;
				} else {
					this.allValid = false;
				}
			},
			priceFormat() {
				let trimmed = this.price.replace(/[^0-9]/g, '');
				let priceArr = trimmed.split('');

				if(priceArr.length > 3) {
					let result = [];
					let lastThree;
					let tripleDigits = []

					while(priceArr.length > 3) {
						lastThree = priceArr.splice(priceArr.length - 3);
						tripleDigits.unshift(lastThree);
					}

					tripleDigits.forEach((item) => {
						item.forEach(digit => {
							result.push(digit);
						})
					})

					if(result.length % 3 === 0 && result.length !== 3) {
						result = result.map((item, index) => {
							if(index !== result.length - 1 && ++index % 3 === 0) {
								return item += " ";
							}
							return item;
						})
					}

					result = priceArr.join('') + " " + result.join("")
					this.price = result;
				} else {
					this.price = trimmed;
				}
				this.checkValid();
			}
		},
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
			margin-bottom: 16px;
			display: block;
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
			&-text {
				font-weight: 400;
				color: #FF8484;
				margin: 4px 0 0;
				font-size: 12px;
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
		box-sizing: border-box;
		transition: 0.3s;
		&::placeholder {
			color: #B4B4B4;
		}
		&:focus {
			border-color:#3F3F3F; 
		}
	}
	&-input-invalid {
		border-color: #FF8484 !important;
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
		&-active {
			box-shadow: inset 1px 1px 10px #333;
		}
	}
}
</style>
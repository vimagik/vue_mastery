<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="currentImage"
             v-on:mouseover="changeColortoGreen"
             v-on:mouseleave="changeColorToBlue"
             alt="">
      </div>
      <div class="product-info">
        <div class="cart">Корзина ({{ cart }})</div>
        <h1>{{ product }}</h1>

        <p v-if="productCount > 10">Товара много в наличии</p>
        <p v-else-if="productCount > 0 && productCount <=10">Осталось совсем немного</p>
        <p v-else>Все закончилось</p>

        <p>{{ description }}</p>

        <a v-bind:href="urlForProduct">Подробное описание продукта</a>

        <div class="colorGroup">
          <span v-for="(c, index) of color"
                :key="index"
                class="colorOfProduct color-circle"
                :style="{backgroundColor: c}"
                @click="changeColor(index)">
          </span>
        </div>

        <p style="padding-top: 10px">Доступные размеры:
          <span v-for="(elemets, i) of avaliableSizes" v-bind:key="i">
            <span>{{ elemets }}</span>
            <span v-if="i !== avaliableSizes.length - 1">, </span>
          </span>
        </p>

        <button
            class="button"
            :disabled="productCount === 0"
            :class="productCount === 0 ? 'disabledButton' : ''"
            @click="cart = cart + 1"
        >Купить</button>
        <button class="button" @click="clearBusket">Очистить</button>
      </div>
    </div>

  </div>
</template>

<script>

import image from './../assets/socks_green.jpg'
import imageBlue from './../assets/socks_blue.jpg'

export default {

  name: "MainComp",
  data() {
    return {
      title: 'Мок компонент круто',
      product: 'Крутые носки',
      description: 'Назначение (вид): На каждый день. Прикольные ' +
          'Особенности носков: однотонные. Материал: 80% хлопок, 20% полиамид',
      productImage: {
        green: image,
        blue: imageBlue
      },
      currentImage: imageBlue,
      urlForProduct: 'https://l-a-b-a.com/lecture/1753-avtomatizacia-processov',
      productCount: 0,
      avaliableSizes: [38, 39, 40, 41, 42],
      cart: 0,
      color: ['green', 'blue']
    }
  },

  methods: {
    changeColortoGreen() {
      this.currentImage = this.productImage.green;
    },
    changeColorToBlue() {
      this.currentImage = this.productImage.blue;
    },
    changeColor(index) {
      if (index === 0) {
        this.changeColortoGreen();
      } else {
        this.changeColorToBlue();
      }
    },
    clearBusket() {
      this.cart = 0;
    }
  }
}
</script>

<style scoped>
body {
  background-color: #f2f2f2;
  margin: 0px;
  font-family: tahoma;
  color: #282828;
}

.button {
  margin: 30px;
  background-color: #39495c;
  border-radius: 5px;
  font-size: 18px;
  width: 160px;
  height: 60px;
  color: white;
  padding: 20px;
  box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
  inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
  inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
}

.cart {
  margin: 25px 100px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 10px 30px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

.color-circle {
  width: 50px;
  height: 50px;
  margin-top: 8px;
  border: 2px solid #d8d8d8;
  border-radius: 50%;
}

.color-circle:hover {
  cursor: pointer;
}


.colorGroup {
  padding: 20px;
}


.disabledButton {
  background-color: #d8d8d8;
  cursor: not-allowed;
}

h1 {
  font-size: 50px;
}

h3 {
  font-size: 25px;
}

img {
  border: 2px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  padding: 15px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

input {
  width: 100%;
  height: 40px;
  margin-bottom: 20px;
}

label {
  font-size: 20px;
  margin-bottom: 5px;
}

li {
  font-size: 18px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 25px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.57);
}

.out-of-stock-img {
  opacity: 0.5
}

p {
  font-size: 22px;
}

.product-display {
  display: flex;
  flex-direction: column;
  padding: 1rem;
}

.product-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.product-image,
.product-info {
  width: 50%;
}

.review-form {
  display: flex;
  flex-direction: column;
  width: 425px;
  padding: 20px;
  margin: 40px;
  border: 2px solid #d8d8d8;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

.review-container {
  width: 425px;
  padding: 20px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 20px -12px rgba(0, 0, 0, 0.57);
  margin-left: 40px;
  border: 2px solid #d8d8d8;
}

.review-container li {
  margin-bottom: 30px;
}

.review-form .button {
  display: block;
  margin: 30px auto;
}

select {
  height: 40px;
  font-size: 20px;
  background-color: white;
  cursor: pointer;
}

textarea {
  width: 95%;
  height: 70px;
  padding: 10px;
  font-size: 20px;
  margin-bottom: 20px;
}

ul {
  list-style-type: none;
}

.colorOfProduct {
  padding: 10px;
  color: blue;
}

@media only screen and (max-width: 600px) {
  .container {
    flex-direction: column;
  }

  .product-image,
  .product-info {
    margin-left: 10px;
    width: 100%;
  }

  .review-form {
    width: 90%;
  }
}

</style>
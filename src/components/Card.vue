<template>
  <div class="card" v-bind:class="{'card--sold': !!isSold}">
    <img v-bind:src="source" v-bind:alt="alt" width="560" height="320">
    <div class="card__description">
      <span class="card__name">{{ name }}</span>
      <span class="card__author">{{ author }}</span>
    </div>
    <div v-if="!isSold" class="card__purchase">
      <div class="card__prices">
        <span v-if="!!oldPrice" class="card__price card__price--old">{{ new Intl.NumberFormat('fr-FR').format(oldPrice) }}</span>
        <span class="card__price">{{ new Intl.NumberFormat('fr-FR').format(price)}}</span>
      </div>
      <button v-if="purchasing" class="custom_button custom_button--purchasing">
        <svg class="loader" version="1.1" id="L4" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
             viewBox="0 0 100 100" enable-background="new 0 0 0 0" xml:space="preserve">
  <circle fill="#fff" stroke="none" cx="6" cy="50" r="6">
    <animate
      attributeName="opacity"
      dur="1s"
      values="0;1;0"
      repeatCount="indefinite"
      begin="0.1"/>
  </circle>
          <circle fill="#fff" stroke="none" cx="26" cy="50" r="6">
    <animate
      attributeName="opacity"
      dur="1s"
      values="0;1;0"
      repeatCount="indefinite"
      begin="0.2"/>
  </circle>
          <circle fill="#fff" stroke="none" cx="46" cy="50" r="6">
    <animate
      attributeName="opacity"
      dur="1s"
      values="0;1;0"
      repeatCount="indefinite"
      begin="0.3"/>
  </circle>
</svg>
      </button>
      <button v-else-if="!inCart" class="custom_button" @click="purchase">Купить</button>
      <button v-else class="custom_button custom_button--in_cart" @click="remove">В корзине</button>
    </div>
    <div v-else class="card__purchase">
      <span class="card__sold">Продана на аукционе</span>
    </div>
  </div>
</template>

<script lang="ts">
import {ADD_TO_CART, DELETE_FROM_CART} from "@/main";

export type CardType = {
  id: number,
  source: string,
  alt: string,
  name: string,
  author: string,
  oldPrice?: number,
  price: number,
  isSold: false,
} | {
  id: number,
  source: string,
  alt: string,
  name: string,
  author: string,
  isSold: true,
}
export default {
  name: "Card",
  props: {
    id: Number,
    source: String,
    alt: String,
    name: String,
    author: String,
    oldPrice: Number,
    price: Number,
    isSold: Boolean,
  },
  data: () => ({
    inCart: false,
    purchasing: false,
  }),
  methods: {
    purchase(){
      this.purchasing = true;
      setTimeout(() => {
        console.log(this.$props)
        this.$store.commit(ADD_TO_CART, this.$props.id)
        this.purchasing = false;
        this.inCart = true;
      }, 2000)
    },
    remove(){
      this.inCart = false;
      this.$store.commit(DELETE_FROM_CART, this.$props.id)
    }
  }
}
</script>

<style scoped>

.loader{
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 2em;
  margin-left: 1em;
  margin-top: .5em;
  background-color: rgba(0, 0, 0, 0);
  text-align: center;
}

</style>

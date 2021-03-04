<template>
  <li class="catalog__item">
    <router-link
      class="catalog__pic"
      :to="{name: 'product', params: {id: product.id}}"
      @click.prevent="gotoPage('product', {id: product.id})"
    >
      <img :src="product.src" :alt="product.title" />
    </router-link>

    <h3 class="catalog__title">
      <a href="#">
        {{ product.title }}
      </a>
    </h3>

    <span class="catalog__price">
      {{ product.price | numberFormat }} ₽
    </span>
  </li>
</template>

<script>
import gotoPage from '@/helpers/gotoPage';
import numberFormat from '@/helpers/numberFormat';

export default {
  name: "ProductItem",
  props: ["product"],
  filters: {
    numberFormat
  },
  methods: {
    gotoPage
  },
};
</script>
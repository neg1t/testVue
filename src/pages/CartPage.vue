<template>
  <main class="content container" v-if="products.length">
    <div class="content__top">
      <ul class="breadcrumbs">
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link" href="index.html"> Каталог </a>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link"> Корзина </a>
        </li>
      </ul>

      <h1 class="content__title">Корзина</h1>
      <span class="content__info"> {{ products.length }} {{ products.length | wordFormat(['товар', 'товара', 'товаров'])}} </span>
    </div>

    <section class="cart">
      <form class="cart__form form" action="#" method="POST">
        <div class="cart__field">
          <ul class="cart__list">
            <CartItem v-for="item in products" :item="item" :key="item.productId" />
          </ul>
        </div>

        <div class="cart__block">
          <p class="cart__desc">
            Мы&nbsp;посчитаем стоимость доставки на&nbsp;следующем этапе
          </p>
          <p class="cart__price">Итого: <span>{{ totalPrice | numberFormat }} ₽</span></p>

          <button class="cart__button button button--primery" type="submit">
            Оформить заказ
          </button>
        </div>
      </form>
    </section>
  </main>
  <main v-else>
    <h1>Корзина пуста</h1>
  </main>
</template>

<script>

import { mapGetters } from 'vuex';
import CartItem from '@/components/CartItem';
import numberFormat from '@/helpers/numberFormat';
import wordFormat from '@/helpers/wordFormat';

export default {
  components: {CartItem},
  computed: {
    ...mapGetters({products: 'cartDetailProducts', totalPrice: 'cartTotalPrice'}),
  },
  filters: {
    numberFormat,
    wordFormat
  },
}
</script>
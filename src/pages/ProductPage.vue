<template>
  <main class="content container">
    <div class="content__top">
      <ul class="breadcrumbs">
        <li class="breadcrumbs__item">
          <router-link class="breadcrumbs__link" :to="{ name: 'main' }">
            Каталог
          </router-link>
        </li>
        <li class="breadcrumbs__item">
          <router-link class="breadcrumbs__link" :to="{ name: 'main' }">
            {{ category.title }}
          </router-link>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link"> {{ product.title }} </a>
        </li>
      </ul>
    </div>

    <section class="item">
      <div class="item__pics pics">
        <div class="pics__wrapper">
          <img
            width="570"
            height="570"
            :src="product.src"
            :alt="product.title"
          />
        </div>
        <ul class="pics__list">
          <li class="pics__item">
            <a href="" class="pics__link pics__link--current">
              <img
                width="98"
                height="98"
                :src="product.src"
                :alt="product.title"
              />
            </a>
          </li>
        </ul>
      </div>

      <div class="item__info">
        <span class="item__code">Артикул: {{ product.id }}</span>
        <h2 class="item__title">{{ product.title }}</h2>
        <div class="item__form">
          <form
            class="form"
            action="#"
            method="POST"
            @submit.prevent="addToCart"
          >
            <b class="item__price"> {{ product.price | numberFormat }} ₽ </b>

            <div class="item__row">
              <div class="form__counter">
                <button
                  type="button"
                  aria-label="Убрать один товар"
                  @click.prevent="deleteOneProduct"
                >
                  <svg width="12" height="12" fill="currentColor">
                    <use xlink:href="#icon-minus"></use>
                  </svg>
                </button>

                <input type="text" v-model.number="productAmount" />

                <button
                  type="button"
                  aria-label="Добавить один товар"
                  @click.prevent="addOneProduct"
                >
                  <svg width="12" height="12" fill="currentColor">
                    <use xlink:href="#icon-plus"></use>
                  </svg>
                </button>
              </div>

              <button class="button button--primery" type="submit">
                В корзину
              </button>
            </div>
          </form>
        </div>
      </div>

      <div class="item__desc">
        <ul class="tabs">
          <li class="tabs__item">
            <a class="tabs__link tabs__link--current"> Описание </a>
          </li>
          <li class="tabs__item">
            <a class="tabs__link" href="#"> Характеристики </a>
          </li>
          <li class="tabs__item">
            <a class="tabs__link" href="#"> Гарантия </a>
          </li>
          <li class="tabs__item">
            <a class="tabs__link" href="#"> Оплата и доставка </a>
          </li>
        </ul>
      </div>
    </section>
  </main>
</template>

<script>
import products from "@/data/products";
import categories from "@/data/categories";
import numberFormat from "@/helpers/numberFormat";

export default {
  model: {
    prop: "productAmount",
    event: "addOneProduct",
  },
  data() {
    return {
      productAmount: 1,
    };
  },
  filters: {
    numberFormat,
  },
  computed: {
    product() {
      return products.find((product) => product.id === +this.$route.params.id);
    },
    category() {
      return categories.find(
        (category) => category.id === this.product.categoryId
      );
    },
  },
  methods: {
    addToCart() {
      this.$store.commit("addProductToCart", {
        productId: this.product.id,
        amount: this.productAmount,
      });
    },
    deleteOneProduct() {
      if (this.productAmount > 1) {
        this.productAmount -= 1;
      }
    },
    addOneProduct() {
      this.productAmount += 1;
    },
  },
};
</script>
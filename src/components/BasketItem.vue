<template>
  <div>
    <div class="product__pic">
      <img
        :src="itemImgUrl"
        width="120"
        height="120"
        :alt="item.product.title"
      />
    </div>

    <h3 class="product__title">
      <router-link :to="{ name: 'product', params: { id: item.product.id } }">
        {{ item.product.title }}
      </router-link>
    </h3>

    <p class="product__info product__info--color">
      Цвет:
      <span>
        <i :style="{'background-color': item.color.color.code}"></i>
        {{ item.color.color.title }}
      </span>
    </p>

    <span class="product__code">
      <p>Размер: {{ item.size.title }}</p>
      <p>Артикул: {{ item.product.id }}</p>
    </span>

    <ProductCount v-model="amount"/>

    <b class="product__price"> {{ computedPrice | numberFormat }} ₽ </b>

    <button
      class="product__del button-del"
      type="button"
      aria-label="Удалить товар из корзины"
      @click.prevent="delItem"
    >
      <svg width="20" height="20" fill="currentColor">
        <use xlink:href="#icon-close"></use>
      </svg>
    </button>
  </div>
</template>

<script>
import ProductCount from "@/components/ProductCount.vue";
import numberFormat from "@/helpers/numberFormat";
import { mapState, mapActions } from "vuex";

export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  components: {
    ProductCount,
  },
  filters: {
    numberFormat,
  },
  data() {
    return {
      amount: this.item.quantity,
    };
  },
  computed: {
    ...mapState({
      basketData: (state) => state.moduleBasket.basketData,
    }),
    computedPrice() {
      return this.item.price * this.amount;
    },
    itemImgUrl() {
      return this.item.color.gallery ? this.item.color.gallery[0].file.url : '/online-store-m/img/not-img.webp';
    },
  },
  methods: {
    ...mapActions({
      changeBasket: "moduleBasket/changeBasket",
      deleteFromBasket: "moduleBasket/deleteFromBasket",
    }),
    delItem() {
      const basketItemId = this.basketData.items.find((p) => p.id === this.item.id).id;
      this.deleteFromBasket({
        basketItemId,
      });
    },
  },
  watch: {
    amount(value) {
      const basketItemId = this.basketData.items.find((p) => p.id === this.item.id).id;
      this.changeBasket({
        basketItemId,
        quantity: value,
      });
    },
  },
};
</script>

<style scoped lang="stylus">
.product > div {
  display: grid;
  grid-template-columns: 120px 280px 140px auto 20px;
  align-items: center;
  grid-gap: 10px 20px;
}
.product__del {
  cursor: pointer;
}
.product__info--color > span > i {
  border: 1px solid #bbb;
}
</style>

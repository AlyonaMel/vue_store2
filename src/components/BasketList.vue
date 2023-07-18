<template>
  <div>
    <ul class="cart__list">
      <li class="cart__item product" v-for="item in basketItems" :key="item.id">
        <BasketItem :item="item" />
      </li>
    </ul>
  </div>
</template>

<script>
import BasketItem from "@/components/BasketItem.vue";
import { mapState } from "vuex";

export default {
  props: {
    basketItems: {
      type: Array,
      required: true,
    },
  },
  components: {
    BasketItem,
  },
  computed: {
    ...mapState({
      basketChangeFail: (state) => state.moduleBasket.basketChangeFail,
      isBasketDeleteSuccess: (state) => state.moduleBasket.isBasketDeleteSuccess,
    }),
  },
  watch: {
    isBasketDeleteSuccess(value) {
      if (value) {
        this.$notify("Товар удалён из корзины");
      }
    },
    basketChangeFail(value) {
      if (value) {
        this.$notify({
          text: `Произошла ошибка: ${value}`,
          type: 'error',
        });
      }
    },
  },
};
</script>

<style scoped lang="stylus">
.product {
  display: block;
}
</style>

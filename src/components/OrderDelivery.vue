<template>

  <transition name="fade" mode="out-in">
    <div v-if="isDeliveriesDataLoading"
        key="isDeliveriesDataLoading"
        class="note__centered"
    >
      <fulfilling-bouncing-circle-spinner
        :animation-duration="4000"
        :size="30"
        :color="'#e02d71'"
      />
      <br/>
      Данные по доставке загружаются...
    </div>

    <div v-else-if="deliveriesDataLoadingFail"
        key="deliveriesDataLoadingFail"
        class="note__error note__centered"
    >
      Произошла ошибка загрузки доставок<br>
      "{{ deliveriesDataLoadingFail }}"<br/><br/>
      <button type="button" class="custom-button" @click.prevent="loadDeliveriesData()">
        Попробуйте еще раз
      </button>
    </div>

    <div v-else
        key="deliveriesData"
        class="deliveries__block"
    >
      <h3 class="cart__title">Доставка</h3>
      <ul class="cart__options options">
        <li class="options__item" v-for="delivery in deliveries" :key="delivery.id">
          <label class="options__label">
            <input
              class="options__radio sr-only"
              type="radio"
              name="delivery"
              :value="delivery.id"
              v-model="computedDeliveryTypeId"
              :checked="delivery.id === 1"
            >
            <span class="options__value">
              {{ delivery.title }} <b>{{ delivery.price | numberFormat }} ₽</b>
            </span>
          </label>
        </li>
      </ul>
    </div>
  </transition>

</template>

<script>
import { mapActions, mapState } from "vuex";
import numberFormat from "@/helpers/numberFormat";
import { FulfillingBouncingCircleSpinner } from "epic-spinners";

export default {
  props: {
    deliveryTypeId: {
      type: Number,
      required: true,
    },
  },
  filters: {
    numberFormat,
  },
  components: {
    FulfillingBouncingCircleSpinner,
  },
  computed: {
    ...mapState({
      deliveriesData: (state) => state.moduleDeliveries.deliveriesData,
      isDeliveriesDataLoading: (state) => state.moduleDeliveries.isDeliveriesDataLoading,
      deliveriesDataLoadingFail: (state) => state.moduleDeliveries.deliveriesDataLoadingFail,
    }),
    deliveries() {
      return this.deliveriesData ? this.deliveriesData : [];
    },
    computedDeliveryTypeId: {
      get() {
        return this.deliveryTypeId;
      },
      set(value) {
        this.$emit("update:deliveryTypeId", value);
      },
    },
  },
  methods: {
    ...mapActions({
      loadDeliveriesData: "moduleDeliveries/loadDeliveriesData",
    }),
  },
  created() {
    this.loadDeliveriesData();
  },
};
</script>

<style scoped lang="stylus"></style>

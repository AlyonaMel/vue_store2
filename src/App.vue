<template>
  <div>
    <BaseHeader />

    <router-view />

    <BaseFooter />
  </div>
</template>

<script>
import BaseHeader from "@/components/BaseHeader.vue";
import BaseFooter from "@/components/BaseFooter.vue";
import { mapMutations, mapActions } from "vuex";

export default {
  components: {
    BaseHeader,
    BaseFooter,
  },
  methods: {
    ...mapMutations(["moduleUser/updateUserAccessKey"]),
    ...mapActions(["moduleBasket/loadBasketData"]),
  },
  created() {
    const userAccessKey = localStorage.getItem("userAccessKey");
    if (userAccessKey) {
      this.$store.commit("moduleUser/updateUserAccessKey", userAccessKey);
      this.$store.dispatch("moduleBasket/loadBasketData", userAccessKey);
    }
  },
};
</script>

<style lang="stylus">
.content
  min-height calc(100vh - 442px)

.note
  &__error
    color red

  &__centered
    text-align center
    font-size 14px

    .fulfilling-bouncing-circle-spinner
      margin 0 auto

.fade-enter-active,
.fade-leave-active
  transition: opacity .3s ease

.fade-enter,
.fade-leave-to
  opacity: 0

.notification
  background #319171 !important
  color #fff
  margin 5px 0 0 0
  border-radius 5px
  padding 8px 12px
  text-align center !important

  &.error
    background #ad3c34 !important

  &-content
    > p
      display block
      margin 0 0 6px 0

    > a
      color #ffffff
      text-decoration underline

      &:hover
        text-decoration none

.custom-button
  display inline-block
  background #e02d71
  border none
  font-size 15px
  line-height 1
  color #fff
  padding 12px 20px
  cursor pointer

  &:hover
    background #150C26
</style>

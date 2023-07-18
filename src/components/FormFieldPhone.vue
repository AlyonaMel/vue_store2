<template>
  <div class="form__label">
    <PhoneMaskInput
      type="tel"
      :name="name"
      :placeholder="placeholder"
      v-model="computedData"
      autoDetectCountry
      inputClass="form__input"
      wrapperClass="form__input-phone-wrapper"
    />
    <span class="form__value">{{ title }}</span>
    <span class="form__error">{{ error }}</span>
  </div>
</template>

<script>
import formFieldMixin from "@/mixins/formFieldMixin";
import PhoneMaskInput from "vue-phone-mask-input";

export default {
  mixins: [
    formFieldMixin,
  ],
  components: {
    PhoneMaskInput,
  },
};
</script>

<style scoped lang="stylus"></style>

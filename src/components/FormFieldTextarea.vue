<template>
  <label class="form__label">
    <textarea
      class="form__input form__input--area"
      :name="name"
      :placeholder="placeholder"
      v-model="computedData"
    ></textarea>
    <span class="form__value">{{ title }}</span>
    <span class="form__error">{{ error }}</span>
  </label>
</template>

<script>
import formFieldMixin from "@/mixins/formFieldMixin";

export default {
  mixins: [
    formFieldMixin,
  ],
};
</script>

<style scoped></style>

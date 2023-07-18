<template>
  <label class="form__label">
    <input
      class="form__input"
      :type="type"
      :name="name"
      :placeholder="placeholder"
      v-model="computedData"
    >
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
  props: {
    type: {
      type: String,
      default: 'text',
    },
  },
};
</script>

<style scoped></style>

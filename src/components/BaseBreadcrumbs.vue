<template>
  <div>
    <ul class="breadcrumbs">
      <li class="breadcrumbs__item" v-for="(page, n) in pages" :key="n">
        <router-link class="breadcrumbs__link" :to="{ name: page.name, params: page.params }">
          {{ page.title }}
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pages: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped></style>

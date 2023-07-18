<template>
  <ul class="catalog__pagination pagination">
    <li class="pagination__item">
      <button
        class="pagination__link pagination__link--arrow"
        :class="{ 'pagination__link--disabled': currentPage === 1 }"
        aria-label="Предыдущая страница"
        @click="gotoPage(currentPage - 1)"
      >
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-left"></use>
        </svg>
      </button>
    </li>

    <li class="pagination__item" v-for="page in countPages" :key="page">
      <button
        class="pagination__link"
        :class="{ 'pagination__link--current': page === currentPage }"
        @click="gotoPage(page)"
      >
        {{ page }}
      </button>
    </li>

    <li class="pagination__item">
      <button
        class="pagination__link pagination__link--arrow"
        :class="{ 'pagination__link--disabled': currentPage === countPages }"
        aria-label="Следующая страница"
        @click="gotoPage(currentPage + 1)"
      >
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-right"></use>
        </svg>
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    value: {
      type: Number,
      required: true,
      default: 1,
    },
    count: {
      type: Number,
      required: true,
    },
    perPage: {
      type: Number,
      required: true,
    },
  },
  computed: {
    countPages() {
      return Math.ceil(this.count / this.perPage);
    },
    currentPage: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit("input", value);
      },
    },
  },
  methods: {
    gotoPage(page) {
      this.currentPage = page > 0 && page <= this.countPages ? page : this.currentPage;
    },
  },
};
</script>

<style scoped lang="stylus">
.pagination__link {
  background: none;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}
.pagination__link:hover {
  outline: 1px solid #eee;
}
.pagination__link--current {
  cursor: default;
  outline: none !important;
}
.pagination__link--disabled {
  cursor: default;
  outline: none !important;
  opacity: 0.5;
}
</style>

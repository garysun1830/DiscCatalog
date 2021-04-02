<template>
  <nav class="pagination" role="navigation">
    <a class="pagination-previous" @click="click_prev">Previous</a>
    <a class="pagination-next" @click="click_next">Next page</a>
    <ul class="pagination-list">
      <li>
        <a :class="page_class(0)" @click="click_page_icon(0)">{{ 1 }}</a>
      </li>
      <li v-if="full_page">
        <span class="pagination-ellipsis">&hellip;</span>
      </li>
      <li v-if="multiple_page(1)">
        <a :class="page_class(1)" @click="click_page_icon(1)">{{ p1 }}</a>
      </li>
      <li v-if="multiple_page(2)">
        <a :class="page_class(2)" @click="click_page_icon(2)">{{ p2 }}</a>
      </li>
      <li v-if="multiple_page(3)">
        <a :class="page_class(3)" @click="click_page_icon(3)">{{ p3 }}</a>
      </li>
      <li v-if="full_page">
        <span class="pagination-ellipsis">&hellip;</span>
      </li>
      <li v-if="multiple_page(0)">
        <a :class="page_class(4)" @click="click_page_icon(4)">{{
          page_total
        }}</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Pagination",
  data() {
    return {
      page_total: 1,
      page_selected: 1,
      p1: 1,
      p2: 1,
      p3: 1,
    };
  },
  props: [],
  components: {},
  created() {
    this.click_page_icon(0);
  },
  methods: {
    multiple_page(n) {
      return this.page_total > n + 1;
    },
    click_page_icon(n) {
      let page_n = [1, this.p1, this.p2, this.p3, this.page_total];
      this.click_page(page_n[n]);
    },
    click_page(page_n) {
      this.$emit("page_clicked", page_n);
    },
    refresh(page_total, page_n) {
      this.page_total = page_total;
      this.page_selected = page_n;
      this.p1 =
        this.page_selected == 1
          ? 2
          : this.page_selected == 2
          ? 2
          : this.page_selected - 1;
      this.p2 = this.p1 + 1;
      this.p3 = this.p2 + 1;
    },
    page_class(n) {
      let result = "pagination-link";
      switch (n) {
        case 0:
          return this.page_selected == 1 ? `${result} is-current` : result;
        case 1:
          return this.page_selected == 2 ? `${result} is-current` : result;
        case 2:
          return this.page_selected > 2 &&
            this.page_selected < this.page_total - 1
            ? `${result} is-current`
            : result;
        case 3:
          return this.page_selected == this.page_total - 1
            ? `${result} is-current`
            : result;
        case 4:
          return this.page_selected == this.page_total
            ? `${result} is-current`
            : result;
      }
    },
    click_prev() {
      if (this.page_selected > 1) {
        this.click_page(this.page_selected - 1);
      }
    },
    click_next() {
      if (this.page_selected < this.page_total) {
        this.click_page(this.page_selected + 1);
      }
    },
  },
  computed: {
    full_page() {
      return this.page_total > 5;
    },
  },
};
</script>

<style scoped>
.pagination {
  padding: 40px;
}
.pagination .pagination-next,
.pagination .pagination-previous {
  padding-left: 1.25em;
  padding-right: 1.25em;
}
</style>
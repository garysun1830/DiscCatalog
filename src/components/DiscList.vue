<template>
  <div>
    <div class="main-div" @click="click_base">
      <div class="tile is-ancestor">
        <div class="tile is-parent">
          <article class="tile is-child box is-1 title-bar">编号</article>
          <article class="tile is-child box is-2 title-bar">名称</article>
          <article class="tile is-child box is-5 title-bar">内容</article>
          <article class="tile is-child box is-2 title-bar">介质</article>
          <article class="tile is-child box is-2 title-bar">位置</article>
        </div>
      </div>
      <DiscItem
        v-for="disc in discs"
        :key="disc.id"
        :item="disc"
        :last_item="disc.last_item"
      />
      <div class="notification is-danger" v-if="has_error">
        {{ error_message }}
      </div>
    </div>
    <Pagination @page_clicked="pagination_change" ref="pagination" />
  </div>
</template>

<script>
import DiscItem from "../components/DiscItem.vue";
import commonMothods from "../../src/commonMothod";
import Pagination from "../components/Pagination.vue";

export default {
  name: "DiscList",
  data() {
    return {
      discs: [],
      page_count: 30,
      has_error: false,
      error_message: null,
    };
  },
  props: {},
  components: { DiscItem, Pagination },
  methods: {
    calc_page_total(count) {
      var quotient = Math.floor(count / this.page_count);
      var remainder = count % this.page_count;
      return remainder == 0 ? quotient : quotient + 1;
    },
    click_base() {
      console.log("main.click_base");
      this.$emit("clicked");
    },
    pagination_change(n) {
      this.refresh(n);
    },
    refresh(page_n) {
      this.has_error = false;
      let url = "disc/count/1/";
      commonMothods.callAPI(
        url,
        "get",
        null,
        (data) => {
          if (isNaN(data)) {
            this.error_message = data;
            this.has_error = true;
            return;
          }
          let page_total = this.calc_page_total(data);
          if (page_n > page_total) {
            page_n = page_total;
          }
          url = `disc/list/1/${page_n}/${this.page_count}/`;
          commonMothods.callAPI(url, "get", null, (data) => {
            this.discs = [...data];
            this.discs[this.discs.length - 1].last_item = "last_item";
            this.$refs["pagination"].refresh(page_total, page_n);
          });
        },
        (error) => {
          this.error_message = error;
          this.has_error = true;
        }
      );
    },
  },
  created() {},
};
</script>

<style scoped>
.main-div {
  margin: 0 10px;
  padding-top: 10px;
}
.tile {
  text-align: center;
}
.title-bar {
  padding: 4px 0;
  font-weight: bold;
  border: solid 1px #ccc;
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
  border-left: none;
  border-bottom: none;
  border-collapse: collapse;
}
.title-bar:first-child {
  border-left: solid 1px #ccc;
}
.title-bar:not(:first-child) {
  border-top-left-radius: 0;
}
.title-bar:not(:last-child) {
  border-top-right-radius: 0;
}
.tile.is-ancestor,
.tile.is-ancestor:not(:last-child) {
  margin: 0;
}
.tile.is-parent {
  padding: 0;
}
.notification {
  margin-top: 20px;
  text-align: left;
}
</style>
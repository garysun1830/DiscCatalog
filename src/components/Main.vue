<template>
  <div class="container">
    <section class="hero is-navy">
      <div class="hero-head">
        <Menu @OnShowSerchBand="click_menu_search" />
      </div>
    </section>
    <section>
      <article class="panel main-panel" @click.self="click_base">
        <Search ref="search_comp" :visible="search_visible" />
        <DiscList @clicked="click_base" />
      </article>
    </section>
  </div>
</template>

<script>
import Menu from "../components/Menu.vue";
import Search from "../components/Search.vue";
import DiscList from "../components/DiscList.vue";

export default {
  name: "Main",
  data() {
    return { search_visible: true };
  },
  props: {},
  components: { Menu, Search, DiscList },
  methods: {
    click_menu_search() {
      this.search_visible = !this.search_visible;
    },
    click_base() {
      this.$refs.search_comp.base_clicked();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hero.is-navy {
  background-color: #4b6c9e;
  font-weight: 700;
  margin: 0px;
  padding: 0px 0px 0px 20px;
  color: #f9f9f9;
  border: none;
  line-height: 2em;
  font-size: 1.7em;
  text-align: left;
}
.main-panel {
  height: 800px;
}
.box {
  border-radius: 0;
}
</style>

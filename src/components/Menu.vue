  <template>
  <nav class="navbar">
    <div class="navbar-brand">
      光盘硬盘数据仓库
      <span class="navbar-burger" data-target="navbarMenuHeroB">
        <span></span>
        <span></span>
        <span></span>
      </span>
    </div>
    <div class="navbar-menu">
      <div class="navbar-end">
        <a class="navbar-item" @click="click_search()"> 搜索 </a>
        <a class="navbar-item"> 列表 </a>
        <a class="navbar-item"> 编辑存储位置 </a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Menu",
  props: {},
  components: {},
  methods:{
      click_search(){
           this.$emit("OnShowSerchBand");
      },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a.navbar-item {
  color: #dde4ec;
  line-height: 1.35em;
  padding: 4px 20px;
  text-decoration: none;
  white-space: nowrap;
  font-size: 0.65em;
  font-weight: 100;
}
a.navbar-item:hover {
  color: #fff;
}
a.navbar-item:focus,
a.navbar-item:focus-within,
a.navbar-item:hover,
a.navbar-item.is-active {
  background-color: #425067;
}
</style>

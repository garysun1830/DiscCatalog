  <template>
  <div class="dropdown-menu" id="dropdown-menu" role="menu">
    <div class="dropdown-content dropdown-item-all">
      <a
        v-for="item in items"
        :key="item"
        href="#"
        class="dropdown-item"
        @click="clicked(item)"
      >
        {{ item }}
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "DropdownItem",
  props: ["items"],
  data() {
    return {};
  },
  methods: {
    clicked(item) {
      this.$emit("selected", item);
    },
  },
};
</script>

<style scoped>
.dropdown-item-all {
  width: 8em;
  padding: 0;
  border: 1px solid;
  border-color: #dbdbdb;
  border-radius: 4px;
}
.dropdown-item {
  background-color: #fff;
  width: 100%;
}

.dropdown-menu {
  padding-top: 0;
}
</style>

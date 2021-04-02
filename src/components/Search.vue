<template>
  <div :class="'box ' + vis_class" @click.self="base_clicked">
    <div class="field is-horizontal">
      <div class="control has-icons-left search-box" style="width: 17em">
        <input class="input" type="text" placeholder="Search" />
        <span class="icon is-left">
          <i class="fas fa-search" aria-hidden="true"></i>
        </span>
      </div>
      <Dropdown
        v-for="filter in filters"
        :key="filter.id"
        :attrib="filter"
        ref="dropdown_comp"
      />
      <a> <i class="fa fa-search fa-2x" aria-hidden="true"></i></a>
    </div>
  </div>
</template>

<script>
import commonMothods from "../../src/commonMothod";
import Dropdown from "../components/Dropdown.vue";

export default {
  name: "Search",
  props: ["visible"],
  components: { Dropdown },
  data() {
    return {
      settings: [
        {
          items: [],
        },
        {
          items: [],
        },
        {
          items: [],
        },
      ],
      filters: [
        {
          caption: "存储介质",
          items: [],
          id: 1,
          ref_dropdown: "dropdown_comp1",
        },
        {
          caption: "文件类型",
          items: [],
          id: 2,
          ref_dropdown: "dropdown_comp2",
        },
        {
          caption: "媒体类型",
          items: [],
          ref_dropdown: "dropdown_comp3",
          id: 3,
        },
      ],
    };
  },
  methods: {
    updateUI() {
      for (var i = 0; i < 3; i++) {
        this.filters[i].items = [...this.settings[i].items];
      }
    },
    base_clicked() {
      this.filters.forEach((f) =>
        this.$refs.dropdown_comp[f.id - 1].base_clicked()
      );
    },
  },
  created() {
    commonMothods.callAPI("1", "get", null, (data) => {
      this.settings[0] = { items: [...data.MediaType] };
      this.settings[1] = { items: [...data.FileType] };
      this.settings[2] = { items: [...data.DiscType] };
      this.updateUI();
    });
  },
  computed: {
    vis_class() {
      return this.visible ? "is-visible" : "";
    },
  },
};
</script>

<style scoped>
.box {
  display: none;
  margin-bottom: 0;
}
.box.is-visible {
  display: block;
}

.search-box {
  width: 20em;
  margin-right: 20px;
}
.box:not(:last-child) {
  margin-bottom: 0;
}
</style>

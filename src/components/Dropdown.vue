<template>
  <div>
    <span class="caption">{{ attrib.caption }}</span>
    <div :class="main_class">
      <div class="dropdown-trigger">
        <button
          class="button"
          aria-haspopup="true"
          aria-controls="dropdown-menu"
          @click="click_on()"
        >
          <span class="dropdown-caption">{{ text }}</span>
          <span class="icon is-small" @click="click_on()">
            <i class="fas fa-angle-down" aria-hidden="true"></i>
          </span>
        </button>
      </div>
      <DropdownItem :items="attrib.items" @selected="item_selected" />
    </div>
  </div>
</template>

<script>
import DropdownItem from "../components/DropdownItem.vue";

export default {
  name: "Dropdown",
  props: ["attrib"],
  components: { DropdownItem },
  data() {
    return { main_class: "dropdown", text: null };
  },
  methods: {
    click_on() {
      this.main_class = "dropdown is-active";
    },
    base_clicked() {
      this.main_class = "dropdown";
    },
    item_selected(item) {
      this.main_class = "dropdown";
      this.text = item;
    },
  },
};
</script>

<style scoped>
.dropdown {
  text-align: left;
  margin-left: 10px;
  margin-right: 20px;
}
.dropdown-caption {
  width: 5em;
}
.button,
.caption {
  font-size: 0.9em;
  text-align: left;
}
</style>

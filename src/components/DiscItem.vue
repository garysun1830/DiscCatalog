   <template>
  <div class="tile is-ancestor">
    <div class="tile is-parent">
      <article :class="item_class_cmpt(0)">{{ item.Code }}</article>
      <article :class="item_class_cmpt(1)">{{ item.Name }}</article>
      <article :class="item_class_cmpt(2)">{{ item.Title }}</article>
      <article :class="item_class_cmpt(3)">{{ item.Disk }}</article>
      <article :class="item_class_cmpt(4)">{{ item.Location }}</article>
    </div>
  </div>
</template>

<script>
export default {
  name: "DiscItem",
  data() {
    return {
      item_class: [
        "tile is-child box is-1 item",
        "tile is-child box is-2 item",
        "tile is-child box is-5 item",
        "tile is-child box is-2 item",
        "tile is-child box is-2 item",
        "tile is-child box is-2 item",
      ],
    };
  },
  props: ["item", "last_item"],
  components: {},
  methods: {
    item_class_cmpt(i) {
      return this.item_class[i] + " " + this.last_item;
    },
  },
};
</script>

<style scoped>
.item {
  padding: 2px 0;
  border-radius: 0;
  box-shadow: none;
  border: solid 1px #ccc;
  border-left: none;
  border-bottom: none;
  border-collapse: collapse;
}
.item:first-child {
  border-left: solid 1px #ccc;
}
.item.last_item {
  border-bottom: solid 1px #ccc;
}
.tile.is-ancestor,
.tile.is-ancestor:not(:last-child) {
  margin: 0;
}
.tile.is-parent {
  padding: 0;
}
</style>
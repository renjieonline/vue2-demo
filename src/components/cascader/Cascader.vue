<template>
  <div v-click-outside="close">
    <div class="trigger" @click="toggle">
      <slot>{{ result }}</slot>
    </div>
    <cascader-item
      v-if="isVisible"
      :options="options"
      @change="onChange"
      :value="value"
    ></cascader-item>
  </div>
</template>
<script>
import CascaderItem from "../cascader/CascaderItem.vue";
export default {
  name: "Cascader",
  components: { CascaderItem },
  props: {
    value: {
      type: Array,
      default: () => [],
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  directives: {
    clickOutside: {
      inserted(el, bindings) {
        // 只在插入时绑定事件
        document.addEventListener("click", (e) => {
          if (e.target === el || el.contains(e.target)) {
            return;
          }
          bindings.value(); // 点击非自己、或者不是自己的儿子就关闭元素
        });
      },
    },
  },
  data() {
    return {
      isVisible: true,
      result: "",
    };
  },
  methods: {
    close() {
      this.isVisible = false;
    },
    toggle() {
      this.isVisible = !this.isVisible;
    },
    onChange(value) {
      this.result = value.map((item) => item.label).join("/");
      this.$emit("input", value);
    },
  },
};
</script>
<style>
.trigger {
  width: 150px;
  height: 25px;
  border: 1px solid #ccc;
}
.content {
  display: flex;
}
</style>

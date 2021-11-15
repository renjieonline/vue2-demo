<template>
  <div class="cascader-item content">
    <div class="content-left">
      <div v-for="(item, key) in options" :key="key">
        <div @click="select(item)">{{ item.label }}</div>
      </div>
    </div>
    <div class="content-right" v-if="lists && lists.length">
      <CascaderItem
        :options="lists"
        @change="onChange"
        :value="value"
        :level="level + 1"
      ></CascaderItem>
    </div>
  </div>
</template>
<script>
import cloneDeep from "lodash/cloneDeep";
export default {
  name: "CascaderItem",
  props: {
    value: {
      type: Array,
      default: () => [],
    },
    level: {
      type: Number,
      default: 0,
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
    return {};
  },
  computed: {
    lists() {
      if (this.value && this.value[this.level]) {
        // 找到这一项
        let item = this.options.find(
          (item) => item.label === this.value[this.level].label
        );
        // 将儿子进行返回
        if (item && item.children) {
          return item.children;
        }
      }
      return [];
    },
  },
  methods: {
    select(item) {
      let cloneValue = cloneDeep(this.value); // 拷贝
      cloneValue[this.level] = item; // 将层级和数组的结果对应上
      cloneValue.splice(this.level + 1);
      this.$emit("change", cloneValue);
    },
    onChange(value) {
      this.$emit("change", value);
    },
  },
};
</script>
<style>
.cascader-item {
  display: flex;
}
.content-left {
  border: 1px solid #ccc;
  min-height: 100px;
}
.content-right {
  margin-left: -1px;
}
.label {
  width: 60px;
  font-size: 12px;
  line-height: 20px;
  color: #606266;
  padding-left: 10px;
  cursor: pointer;
}
.label:hover {
  background: #f5f7fa;
}
</style>

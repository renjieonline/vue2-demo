<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Cascader :options="options" v-model="selected" />
  </div>
</template>

<script>
import Cascader from "./components/cascader";

export default {
  name: "App",
  components: {
    Cascader,
  },
  data() {
    return {
      selected: [],
      options: [
        {
          label: "肉类",
          value: "meat",
          children: [
            {
              label: "猪肉",
              value: "pork",
              children: [
                {
                  label: "五花肉",
                },
                {
                  label: "里脊肉",
                },
              ],
            },
            {
              label: "鸡肉",
              children: [
                {
                  label: "鸡腿",
                },
                {
                  label: "鸡翅",
                },
              ],
            },
          ],
        },
        {
          label: "蔬菜",
          children: [
            {
              label: "叶菜类",
              children: [
                {
                  label: "大白菜",
                },
                {
                  label: "小白菜",
                },
              ],
            },
            {
              label: "根茎类",
              children: [
                {
                  label: "萝卜",
                },
                {
                  label: "土豆",
                },
              ],
            },
          ],
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

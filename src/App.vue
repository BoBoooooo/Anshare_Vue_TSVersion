<template>
  <div id="app">
    <router-view />
    <router-link to="/about">about</router-link>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class App extends Vue {
  x = 0;

  y = 0;

  count = 0;

  outTime = 0;

  // 此处ts坑,需要指明dom类型
  // loadingNode = document.getElementById('loading') as HTMLElement;

  // beforeCreate() {
  //   document.body.removeChild(this.loadingNode);
  // }

  mounted() {
    // 判断加载哪套主题
    if (localStorage.getItem('customTheme')) {
      document.body.className = 'custom-theme';
    }
    // 全局计时器判断是否长时间未操作
    // this.initEvent();
  }

  initEvent() {
    // 监听鼠标
    document.onmousemove = (event) => {
      const x1 = event.clientX;
      const y1 = event.clientY;
      if (this.x !== x1 || this.y !== y1) {
        this.count = 0;
      }
      this.x = x1;
      this.y = y1;
    };
    // 监听键盘
    document.onkeydown = () => {
      this.count = 0;
    };
    window.setInterval(() => {
      this.count += 1;
      if (this.count === this.outTime * 60) {
        this.$store.dispatch('clearToken');
      }
    }, 1000);
  }
}
</script>
<style lang="scss" scoped>
#nprogress .bar {
  background: red !important; //自定义颜色
}
</style>

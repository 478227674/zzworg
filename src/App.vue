<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>

  export default {
    provide() {    //父组件中通过provide来提供变量，在子组件中通过inject来注入变量。
      return {
        reload: this.reload
      }
    },
    name: 'app',
    methods: {
      reload() {
        this.isRouterAlive = false;            //先关闭，
        this.$nextTick(function () {
          this.isRouterAlive = true;         //再打开
        })
      }
    }
  }
</script>

<style>

</style>

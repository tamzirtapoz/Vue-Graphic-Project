<template>
  <!-- <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
    <router-link to="/login">Login</router-link>
  </div> -->
  <div
    class="container-fluid m-0 p-0"
    @click="resetCounter"
    @keyup="resetCounter"
  >
    <router-view />
  </div>
  <div
    :style="{
      position: 'fixed',
      bottom: '25px',
      right: '25px',
      zIndex: '1500',
      background: 'rgba(255,255,255,1)',
      border: '1px solid rgba(0,0,0,1)',
      padding: '5px',
      color: 'red',
    }"
  >
    {{ timeReamaining }}
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";

export default {
  data() {
    return {
      finishTime: Date.now() + 60 * 1000,
      timeReamaining: 59,
      timerTimeoutFunc: Function,
    };
  },
  computed: {
    ...mapState(["loginStatus"]),
  },
  methods: {
    ...mapActions(["userLoggedOut"]),
    continueCounter() {
      if (this.loginStatus === true) {
        this.timerTimeoutFunc = setTimeout(this.counterDown, 1000);
      }
    },
    counterDown() {
      if (this.finishTime - Date.now() > 0) {
        this.timeReamaining = Math.floor((this.finishTime - Date.now()) / 1000);
        this.continueCounter();
      } else {
        this.timeReamaining = 0;
        this.userLoggedOut();
        setTimeout(() => {
          window.alert("timout");
        }, 500);
      }
    },
    resetCounter() {
      clearTimeout(this.timerTimeoutFunc);
      this.finishTime = Date.now() + 60 * 1000;
      this.timeReamaining = Math.floor(
        (this.finishTime - Date.now()) / 1000 - 1
      );
      this.continueCounter();
    },
  },
  watch: {
    loginStatus: {
      immediate: true,
      handler() {
        this.continueCounter();
      },
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

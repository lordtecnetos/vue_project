<template>
  <div id="app">
    <transition>
      <router-view />
    </transition>
    <Log />
  </div>
</template>

<script>
import Log from "./components/Log";

export default {
  components: {
    Log,
  },
};
</script>

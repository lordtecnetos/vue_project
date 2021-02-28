<template>
  <div>
    <div v-for="(v, k) in items" :key="k">{{ v }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
    };
  },
  methods: {
    push(e) {
      this.items.push(e);
    },
  },
  mounted() {
    this.$root.$on("log", this.push);
  },
};
</script>
<template>
  <div>
    <div v-if="qtd <= 2">
      outro num <b>{{ qtd }}</b>
    </div>

    <Outro :qtd="qtd" />

    <button @click="aumentar()">+1</button>
    <button @click="zerar()" :disabled="qtd == 0">0</button>
  </div>
</template>

<script>
import Outro from "./Outro";
import bell from "@/assets/audio.mp3";

export default {
  components: {
    Outro,
  },
  data() {
    return {
      qtd: 0,
    };
  },
  methods: {
    aumentar() {
      this.$root.$emit("log", "aumetei");
      this.qtd += 1;
    },
    zerar() {
      this.$root.$emit("log", "zerei");
      this.qtd = 0;
    },
  },
  watch: {
    qtd(n) {
      if (n % 3 == 0) {
        new Audio(bell).play();
      }
    },
  },
};
</script>
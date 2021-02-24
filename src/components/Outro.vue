<template>
  <div>
    <div v-if="qtd > 2">
      sou maior q 2 numerão agora <b>{{ qtd }}</b>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    qtd: { type: Number, default: 0 },
  },
};
</script>
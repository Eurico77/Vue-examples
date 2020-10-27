<script>
export default {
  name: "Carousel",
  props: {
    titulo: {
      type: String,
      required: true,
      default: () => "",
    },
    subtitulo: {
      type: String,
      required: true,
      default: () => "",
    },
    position: {
      type: Number,
      required: true,
      default: () => 0,
    },
  },
  data() {
    return {
      qtdItens: 0,
    };
  },
  methods: {
    recuperePosition() {
      const texto = this.textos.find(({ position }) => position === index);
      return texto || null;
    },
  },
};
</script>

<template>
  <div class="shr-carousel">
    <div v-for="(item, index) in qtdItens" :key="item">
      <slot name="`item-${index}`" />
      <div>{{ titulo[index] }}</div>
    </div>
  </div>
</template>

<style scoped>
.shr-carousel {
}
</style>

<script>
export default {
  name: 'ShrCarousel',
  props: {
    titulo: {
      type: String,
      required: true,
      default: () => '',
    },
    subtitulo: {
      type: String,
      required: true,
      default: () => '',
    },
    qtdItens: {
      type: Number,
      required: true,
      default: () => 0,
    },
  },
  data() {
    return {
      itemAtual: 0,
    }
  },
  methods: {},
}
</script>
<template>
  <div class="shr-carousel">
    <div v-for="(item, index) in qtdItens" :key="item">
      <slot :name="`item-${index}`" />
      <template v-if="titulo && subtitulo">
        <div>{{ titulo }}</div>
        <div>{{ subtitulo }}</div>
      </template>
      <slot v-else :name="`item-${index}`" />
    </div>
  </div>
</template>
<style scoped>
.shr-carousel {
  display: flex;
}
</style>

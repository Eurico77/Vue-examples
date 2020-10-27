<template>
  <div class="main">
    <ShrCarousel
      :qtdItens="3"
      :titulo="textos.title"
      :subtitulo="textos.subtitle"
      :navegar-pelas-setas="navegarPelasSetas"
      @change="slideAtual = $event"
    >
      <template v-slot:item-0>aaa</template>
      <template v-slot:item-1>bbb</template>
      <template v-slot:item-2>ccc</template>
    </ShrCarousel>
  </div>
</template>

<script>
import ShrCarousel from "../components/Carousel/Carousel";
export default {
  components: {
    ShrCarousel,
  },
  data() {
    return {
      slideAtual: 0,
      navegarPelasSetas: true,
    };
  },
  computed: {
    textos() {
      if (this.slideAtual === 0)
        return {
          title: "teste 0",
          subtitle: "subtitulo 0",
        };
      else if (this.slideAtual === 1)
        return {
          title: "teste 1",
          subtitle: "subtitulo 1",
        };
      else if (this.slideAtual === 2)
        return {
          title: "teste 2",
          subtitle: "subtitulo 2",
        };
      else
        return {
          title: "",
          subtitle: "",
        };
    },
  },
};
</script>

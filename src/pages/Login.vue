<template>
  <div class="main">
    <ShrCarousel>
      <template slot="titulo"> ssdask </template>
      <template slot="subtitulo"> ssdask </template>
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
      title: "teste",
      subTitle: "titlo teste",
    };
  },
};
</script>

<script>
export default {
  name: "ShrCarousel",
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
    qtdItens: {
      type: Number,
      required: true,
      default: () => 0,
    },
    navegarPelasSetas: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      itemAtual: 0,
      intervalo: null,
    };
  },
  mounted() {
    this.setarIntervalo();
    document.addEventListener("keydown", this.listeningToArrowKeys);
  },
  destroyed() {
    document.removeEventListener("keydown", this.listeningToArrowKeys);
    clearInterval(this.intervalo);
  },
  methods: {
    setarIntervalo() {
      this.intervalo = setInterval(() => this.mudarSlide(), 8000);
    },
    mudarSlide() {
      if (this.itemAtual < this.qtdItens - 1) this.itemAtual++;
      else this.itemAtual = 0;

      this.$emit("change", this.itemAtual);
    },
    listeningToArrowKeys(e) {
      if (this.navegarPelasSetas) {
        const irParaEsquerda = () => {
          if (e.keyCode === 37) {
            this.itemAtual === 0
              ? (this.itemAtual = this.qtdItens - 1)
              : this.itemAtual--;
            clearInterval(this.intervalo);
            this.setarIntervalo();
          }
        };
        const irParaDireita = () => {
          if (e.keyCode === 39) {
            this.itemAtual < this.qtdItens - 1
              ? this.itemAtual++
              : (this.itemAtual = 0);
            clearInterval(this.intervalo);
            this.setarIntervalo();
          }
        };
        irParaEsquerda();
        irParaDireita();
        this.$emit("change", this.itemAtual);
      }
    },
    cliqueNaBolinha(index) {
      this.$emit("change", index);
      this.itemAtual = index;
      clearInterval(this.intervalo);
      this.setarIntervalo();
    },
  },
};
</script>
<template>
  <div class="shr-carousel">
    <div v-for="(item, index) in qtdItens" :key="item">
      <template v-if="itemAtual === index">
        <slot :name="`item-${index}`" />
        <template v-if="titulo && subtitulo">
          <div>{{ titulo }}</div>
          <div>{{ subtitulo }}</div>
        </template>
      </template>
    </div>
    <div class="shr-carousel__dots">
      <span
        v-for="(i, index) in qtdItens"
        class="shr-carousel__dots__dot"
        :class="{ 'shr-carousel__dots__dot--active': itemAtual === index }"
        :key="index"
        @click="cliqueNaBolinha(index)"
      />
    </div>
  </div>
</template>
<style scoped lang="scss">
.shr-carousel {
  &__dots {
    display: flex;
    padding-top: 10px;

    &__dot {
      cursor: pointer;
      height: 10px;
      width: 10px;
      background-color: #e0e0e0;
      border-radius: 100%;
      transition: all 0.2s ease;

      &:not(:last-of-type) {
        margin-right: 10px;
      }

      &:hover {
        transition: all 0.2s ease;
        transform: scale(1.1);
      }

      &--active {
        transform: scale(1.2);
        background-color: blue;
      }
    }
  }
}
</style>

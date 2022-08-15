<template>
  <q-page class="column items-center justify-center">
    <div class="row items-center justify-center">
      <q-carousel
        v-model="slide"
        transition-prev="jump-right"
        transition-next="jump-left"
        swipeable
        animated
        control-color="black"
        prev-icon="arrow_left"
        next-icon="arrow_right"
        navigation-icon="none"
        arrows
        height="200px"
        class="bg-white text-black shadow-1"
      >
        <q-carousel-slide
          v-for="slide in slides"
          :key="slide.name"
          :name="slide.name"
          class="column no-wrap flex-center"
        >
          <carousel-slide :contentColor="slide.color" :title="slide.name" />
        </q-carousel-slide>
      </q-carousel>
      <circular-carousel v-model="next" :key="updateKey">
        <div v-for="slide in slides" :key="slide">
          {{ slide.name }}
        </div>
      </circular-carousel>
      <q-btn color="primary" icon="check" label="OK" @click="nextItem" />
    </div>
  </q-page>
</template>

<script>
import CarouselSlide from "src/components/CarouselSlide.vue";
import CircularCarousel from "src/components/CircularCarousel.vue";
import { defineComponent, ref, VueElement } from "vue";

export default defineComponent({
  name: "IndexPage",
  components: { CarouselSlide, CircularCarousel },
  data() {
    return {
      next: false,
      slide: "style",
      colorNum: 0,
      updateKey: 0,
      isSpinning: false,
      slides: [
        {
          name: "first",
        },
        {
          name: "second",
        },
        {
          name: "third",
        },
        {
          name: "fourth",
        },
      ],
    };
  },
  mounted() {
    this.slide = this.slides[0].name;
    this.slides.map((slide, index) => {
      slide.color = `hsl(${(999 * (index + 1)) / this.slides.length},80%, 50%)`;
    });
  },
  methods: {
    nextItem() {
      if (!this.isSpinning) {
        this.isSpinning = true;
        this.next = true;
        const that = this;
        this.slide = this.slides[1].name;
        setTimeout(function () {
          const first = that.slides[0];
          that.slides.shift();
          that.slides.push(first);
          that.updateKey++;
          that.isSpinning = false;
        }, 3000);
      }
    },
  },
});
</script>

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
          <carousel-slide :contentColor="slide.color" />
        </q-carousel-slide>
      </q-carousel>
      <circular-carousel>
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
      </circular-carousel>
    </div>
  </q-page>
</template>

<script>
import CarouselSlide from "src/components/CarouselSlide.vue";
import CircularCarousel from "src/components/CircularCarousel.vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  components: { CarouselSlide, CircularCarousel },
  data() {
    return {
      slide: "style",
      colorNum: 0,
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
        {
          name: "fifth",
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
});
</script>

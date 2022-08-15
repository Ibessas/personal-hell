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
      <circular-carousel
        v-model="next"
        :key="updateKey"
        :animationTime="animationTime"
        :clockwise="clockwise"
      >
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
      animationTime: 250,
      clockwise: true,
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
  methods: {
    nextItem() {
      if (!this.isSpinning) {
        this.isSpinning = true;
        this.next = true;
        const that = this;
        if (this.clockwise) {
          this.slide = this.slides[this.slides.length - 1].name;
        } else {
          this.slide = this.slides[1].name;
        }
        setTimeout(function () {
          if (that.clockwise) {
            that.clockwiseList();
          } else {
            that.counterClockwiseList();
          }
          that.updateKey++;
          that.isSpinning = false;
        }, that.animationTime);
      }
    },
    counterClockwiseList() {
      const first = this.slides[0];
      this.slides.shift();
      this.slides.push(first);
    },
    clockwiseList() {
      const last = this.slides[this.slides.length - 1];
      this.slides.pop();
      this.slides.unshift(last);
    },
  },
});
</script>

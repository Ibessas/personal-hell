<template>
  <div
    class="items-center column"
    :style="{
      color: contentColor,
    }"
  >
    <q-icon name="style" size="56px" />
    <div>{{ title }}</div>
    <div class="q-mt-md text-center">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "CarouselSlide",
  props: {
    contentColor: {
      type: String,
      default: "black",
    },
    title: {
      type: String,
    },
  },
});
</script>

<style>
</style>

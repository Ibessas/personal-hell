<template>
  <div
    class="container text-center"
    :class="{
      parentSpin: parentSpin,
    }"
  >
    <slot></slot>
  </div>
  <q-btn
    color="primary"
    icon="check"
    label="OK"
    @click="(childSpin = !childSpin), (parentSpin = !parentSpin)"
  />
</template>
<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "CircularCarousel",
  data() {
    return {
      childSpin: false,
      parentSpin: false,
    };
  },
  mounted() {
    this.itemPosition();
  },
  watch: {
    childSpin: function (value) {
      if (value) {
        this.$slots.default().forEach((item) => {
          item.el.className = "contentSpin";
        });
      } else {
        this.$slots.default().forEach((item) => {
          item.el.className = "";
        });
      }
    },
  },
  methods: {
    itemPosition() {
      const radius = 50;
      let container = document.getElementsByClassName("container")[0];
      let width = container.style.width;
      let height = container.style.height;
      let fields = Array.from(container.childNodes);
      let angle = 0,
        step = (2 * Math.PI) / (fields.length - 2);
      fields.forEach((el) => {
        if (el.style) {
          let x = Math.round(
            width / 2 + radius * Math.cos(angle) - el.style.width / 2
          );
          let y = Math.round(
            height / 2 + radius * Math.sin(angle) - el.style.height / 2
          );
          el.style.left = x + "px";
          el.style.top = y + "px";
          angle += step;
        }
      });
    },
  },
});
</script>

<style lang="sass">
.parentSpin
  animation: parentSpin 3s

.contentSpin
  animation: contentSpin 3s

.container
  width: 50px
  height: 50px
  margin: 50px
  position: relative
  border-radius: 50%
  border: 1px solid black
  color: #f00
  div
    border: 1px solid red
    position: absolute
    width: 50px
    height: 50px
    color: #000
    border-radius: 50%
    line-height: 50px

@keyframes parentSpin
  100%
    transform: rotate(90deg)
@keyframes contentSpin
  100%
    transform: rotate(-90deg)
</style>

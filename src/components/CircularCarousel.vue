<template>
  <div
    class="container text-center"
    :class="{
      parentSpin: parentSpin,
    }"
  >
    <slot></slot>
  </div>
</template>
<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "CircularCarousel",
  props: {
    modelValue: Boolean,
  },
  emits: ["update:modelValue"],
  data() {
    return {
      childSpin: false,
      parentSpin: false,
    };
  },
  mounted() {
    this.itemPosition();
  },
  computed: {
    totalFields: function () {
      return Array.from(
        document.getElementsByClassName("container")[0].childNodes
      ).filter((el) => el.nodeName !== "#text").length;
    },
  },
  watch: {
    childSpin: function (value) {
      console.log(document.getElementsByClassName("container")[0]);
      if (value) {
        [...document.getElementsByClassName("container")[0].childNodes].forEach(
          (item) => {
            if (item.classList) item.classList.add("contentSpin");
          }
        );
      } else {
        [...document.getElementsByClassName("container")[0].childNodes].forEach(
          (item) => {
            if (item.classList) item.classList.remove("contentSpin");
          }
        );
      }
    },
    modelValue: function (value) {
      if (value) {
        this.doSpin();
        this.$emit("update:modelValue", false);
      }
    },
  },
  methods: {
    doSpin() {
      if (!this.childSpin) {
        const that = this;
        this.childSpin = true;
        this.parentSpin = true;
        setTimeout(function () {
          that.childSpin = false;
          that.parentSpin = false;
          that.$forceUpdate();
        }, 3000);
      }
    },
    itemPosition() {
      const radius = 50;
      let container = document.getElementsByClassName("container")[0];
      let width = container.style.width;
      let height = container.style.height;
      let fields = Array.from(container.childNodes);
      let angle = 0,
        step = (2 * Math.PI) / this.totalFields;
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
    transform: rotate(-72deg)
@keyframes contentSpin
  100%
    transform: rotate(72deg)
</style>

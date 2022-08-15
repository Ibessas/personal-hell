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
    animationTime: Number,
    clockwise: Boolean,
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
    positiveCircleRotation: function () {
      const degrees = this.clockwise
        ? -`${360 / this.totalFields}`
        : `${360 / this.totalFields}`;
      return `rotate(${degrees}deg)`;
    },
    negativeCircleRotation: function () {
      const degrees = this.clockwise
        ? `${360 / this.totalFields}`
        : -`${360 / this.totalFields}`;
      return `rotate(${degrees}deg)`;
    },
    animationParent: function () {
      return `parentSpin ${this.animationTime / 1000}s`;
    },
    animationContent: function () {
      return `contentSpin ${this.animationTime / 1000}s`;
    },
  },
  watch: {
    childSpin: function (value) {
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
        }, that.animationTime);
      }
    },
    itemPosition() {
      const radius = 50;
      let container = document.getElementsByClassName("container")[0];
      let width = container.style.width;
      let height = container.style.height;
      let fields = Array.from(container.childNodes);
      let angle = 0;
      let step = (2 * Math.PI) / this.totalFields;
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
          // if (this.clockwise) {
          //   if (angle === 0) {
          //     angle = step * this.totalFields;
          //   }
          //   angle -= step;
          // } else {
          angle += step;
          // }
        }
      });
    },
  },
});
</script>

<style >
.parentSpin {
  animation: v-bind("animationParent");
}

.contentSpin {
  animation: v-bind("animationContent");
}

.container {
  width: 50px;
  height: 50px;
  margin: 50px;
  position: relative;
  border-radius: 50%;
  border: 1px solid black;
  color: #f00000;
}
.container > div {
  border: 1px solid red;
  position: absolute;
  width: 50px;
  height: 50px;
  color: #000;
  border-radius: 50%;
  line-height: 50px;
}

@keyframes parentSpin {
  100% {
    transform: v-bind("negativeCircleRotation");
  }
}

@keyframes contentSpin {
  100% {
    transform: v-bind("positiveCircleRotation");
  }
}
</style>

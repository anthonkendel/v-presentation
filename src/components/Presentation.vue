<template lang="pug">
  div.presentation(v-if="hasSlides")
    div.content
      VNode(:node="currentSlide")
    div.footer
      span.arrow(@click="previous") ◀
      span {{ currentPage }} out of {{ numberOfSlides }}
      span.arrow(@click="next") ▶
</template>

<script>
import VNode from "@/components/VNode";

export default {
  name: "Presentation",
  components: { VNode },
  data: () => ({
    slides: [],
    index: 0,
    keydownListener: undefined
  }),
  computed: {
    hasSlides: vm => vm.numberOfSlides > 0,
    numberOfSlides: vm => vm.slides.length,
    currentPage: vm => vm.index + 1,
    currentSlide: vm => vm.slides[vm.index]
  },
  methods: {
    init() {
      window.document.addEventListener("keydown", event => {
        if (event.key === "ArrowLeft") {
          this.previous();
        }

        if (event.key === "ArrowRight") {
          this.next();
        }
      });
    },
    previous() {
      if (this.currentPage > 1) {
        this.index--;
      }
    },
    next() {
      if (this.currentPage < this.numberOfSlides) {
        this.index++;
      }
    }
  },
  created() {
    this.slides =
      this.$slots.default.filter(slot => slot.data !== undefined) || [];
    if (this.slides.length > 0) {
      this.init();
    }
  },
  beforeDestroy() {
    if (this.keydownListener) {
      window.document.removeEventListener(this.keydownListener);
    }
  }
};
</script>

<style scoped>
.arrow {
  cursor: pointer;
  margin-left: 1em;
  margin-right: 1em;
}

.arrow:hover {
  transition: 0.2s;
  color: gray;
}

.content {
  padding: 1em;
  margin-left: 30%;
  margin-right: 30%;
  font-size: 1.7em;
}

.footer {
  padding: 1em;
  font-size: 1.2em;
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>

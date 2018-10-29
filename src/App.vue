<template lang="pug">
  #app
    Presentation
      Slide
        h1 Step 1
        p With some text
        ol
          li It
          li can
          li even
          li contain
          li bulletins
      Slide
        h1 Step 2
        p With some new text
        p and an image
        p
          img(src="https://picsum.photos/200")
</template>

<script>
import Presentation from "@/components/Presentation";
import Slide from "@/components/Slide";

export default {
  name: "App",
  components: {
    Presentation,
    Slide
  }
};
</script>

<style>
body {
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen,
    Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
}
</style>

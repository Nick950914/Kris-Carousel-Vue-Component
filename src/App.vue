<template>
  <div id="app">
    <app-carousel :items="items" :suggested="suggestVisit"></app-carousel>
  </div>
</template>

<script>
import Carousel from "./components/Carousel";
export default {
  data() {
    return {
      // This is our main array of items which we pass as a prop to Carousel.vue.
      items: [
        {
          id: 1,
          imgSrc: "http://unsplash.it/140/100/?random",
          description: "Description for item #1."
        },
        {
          id: 2,
          imgSrc: "http://unsplash.it/141/101/?random",
          description: "Description for item #2."
        },
        {
          id: 3,
          imgSrc: "http://unsplash.it/142/102/?random",
          description: "Description for item #3."
        },
        {
          id: 4,
          imgSrc: "http://unsplash.it/143/103/?random",
          description: "Description for item #4."
        },
        {
          id: 5,
          imgSrc: "http://unsplash.it/144/104/?random",
          description: "Description for item #5."
        },
        {
          id: 6,
          imgSrc: "http://unsplash.it/145/105/?random",
          description: "Description for item #6."
        },
        {
          id: 7,
          imgSrc: "http://unsplash.it/146/106/?random",
          description: "Description for item #7."
        },
        {
          id: 8,
          imgSrc: "http://unsplash.it/147/107/?random",
          description: "Description for item #8."
        },
        {
          id: 9,
          imgSrc: "http://unsplash.it/148/108/?random",
          description: "Description for item #9."
        },
        {
          id: 10,
          imgSrc: "http://unsplash.it/149/109/?random",
          description: "Description for item #10."
        }
      ],
      // This is an array of suggested items to visit. Also passed as a prop to Carousel.vue.
      suggestVisit: [
        {
          name: "Hogwarts School of Witchcraft and Wizardry",
          url: "https://www.wizardingworld.com/"
        },
        {
          name: "Lochness Monster's Domain",
          url: "http://www.lochnesssightings.com/"
        },
        {
          name: "The Middle of Nowhere",
          url: "https://en.wikipedia.org/wiki/Middle_of_Nowhere"
        }
      ]
    };
  },
  components: {
    "app-carousel": Carousel
  }
};
</script>

<style>
</style>
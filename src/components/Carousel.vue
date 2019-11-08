<template>
  <div class="carousel-frame mt-5">
    <h6 class="pt-3 pl-3">
      People who viewed this item also viewed
      <a :href="suggestedUrl">{{suggestedName}}</a>
    </h6>
    <div class="top-content pt-4">
      <div class="container-fluid">
        <div
          id="carousel-example"
          class="carousel slide"
          data-interval="false"
          data-ride="carousel"
        >
          <div class="carousel-inner row w-100 mx-auto" role="listbox">
            <CarouselItem v-for="item in items" :item="item" :key="item.id"></CarouselItem>
          </div>
          <!-- Condition for displaying left slider arrow. -->
          <a
            v-if="lengthCheck && initialNumber > 4"
            @click="handleLeftSlide"
            class="carousel-control-prev"
            href="#carousel-example"
            role="button"
            data-slide="prev"
          >
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="sr-only">Previous</span>
          </a>
          <!-- Condition for displaying right slider arrow. -->
          <a
            v-if="lengthCheck && initialNumber < items.length"
            @click="handleRightSlide"
            class="carousel-control-next"
            href="#carousel-example"
            role="button"
            data-slide="next"
          >
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="sr-only">Next</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CarouselItem from "./CarouselItem";
export default {
  props: ["items", "suggested"],
  components: {
    CarouselItem
  },
  data() {
    return {
      suggestedName: "",
      suggestedUrl: "",
      initialNumber: 4
    };
  },
  methods: {
    // This and handleLeftSlide, along with v-if in the template section, is the desired logic to never display a left slide arrow if the left-most element is the first element in the array of items, and right arrow if the right most item is the last element in the array. We use initial number which is equal to the number of items that are displayed per slide (4 in our case, couldn't find a solution to let developers choose a number of their own).
    handleRightSlide() {
      if (this.initialNumber === this.items.length) {
        return;
      } else {
        this.initialNumber++;
      }
    },
    handleLeftSlide() {
      if (this.initialNumber === 4) {
        return;
      } else {
        this.initialNumber--;
      }
    }
  },
  // Length checker (check v-for in the template above).
  computed: {
    lengthCheck() {
      return this.items.length > 4;
    }
  },
  // Chooses a random element from the suggested array, then assigns the respective name and URL to the local data properties.
  created() {
    let randomSuggested = this.suggested[
      Math.floor(Math.random() * this.suggested.length)
    ];
    this.suggestedName = randomSuggested.name;
    this.suggestedUrl = randomSuggested.url;
  }
};
</script>

<style scoped>
.carousel {
  margin: auto;
  width: 900px;
  height: 200px;
}

.carousel-frame {
  margin: auto;
  width: 1000px;
  height: 350px;
  border: 1px solid black;
}

h6 a {
  text-decoration: none;
}

@media (min-width: 768px) and (max-width: 991px) {
  /* Show 4th slide on md if col-md-4*/
  .carousel-inner
    .active.col-md-4.carousel-item
    + .carousel-item
    + .carousel-item
    + .carousel-item {
    position: absolute;
    top: 0;
    right: -33.3333%; /*change this with javascript in the future*/
    z-index: -1;
    display: block;
    visibility: visible;
  }
}
@media (min-width: 576px) and (max-width: 768px) {
  /* Show 3rd slide on sm if col-sm-6*/
  .carousel-inner
    .active.col-sm-6.carousel-item
    + .carousel-item
    + .carousel-item {
    position: absolute;
    top: 0;
    right: -50%; /*change this with javascript in the future*/
    z-index: -1;
    display: block;
    visibility: visible;
  }
}
@media (min-width: 576px) {
  .carousel-item {
    margin-right: 0;
  }
  /* show 2 items */
  .carousel-inner .active + .carousel-item {
    display: block;
  }
  .carousel-inner
    .carousel-item.active:not(.carousel-item-right):not(.carousel-item-left),
  .carousel-inner
    .carousel-item.active:not(.carousel-item-right):not(.carousel-item-left)
    + .carousel-item {
    transition: none;
  }
  .carousel-inner .carousel-item-next {
    position: relative;
    transform: translate3d(0, 0, 0);
  }
  /* left or forward direction */
  .active.carousel-item-left + .carousel-item-next.carousel-item-left,
  .carousel-item-next.carousel-item-left + .carousel-item,
  .carousel-item-next.carousel-item-left + .carousel-item + .carousel-item {
    position: relative;
    transform: translate3d(-100%, 0, 0);
    visibility: visible;
  }
  /* farthest right hidden item must be also positioned for animations */
  .carousel-inner .carousel-item-prev.carousel-item-right {
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    display: block;
    visibility: visible;
  }
  /* right or prev direction */
  .active.carousel-item-right + .carousel-item-prev.carousel-item-right,
  .carousel-item-prev.carousel-item-right + .carousel-item,
  .carousel-item-prev.carousel-item-right + .carousel-item + .carousel-item {
    position: relative;
    transform: translate3d(100%, 0, 0);
    visibility: visible;
    display: block;
    visibility: visible;
  }
}
/* MD */
@media (min-width: 768px) {
  /* show 3rd of 3 item slide */
  .carousel-inner .active + .carousel-item + .carousel-item {
    display: block;
  }
  .carousel-inner
    .carousel-item.active:not(.carousel-item-right):not(.carousel-item-left)
    + .carousel-item
    + .carousel-item {
    transition: none;
  }
  .carousel-inner .carousel-item-next {
    position: relative;
    transform: translate3d(0, 0, 0);
  }
  /* left or forward direction */
  .carousel-item-next.carousel-item-left
    + .carousel-item
    + .carousel-item
    + .carousel-item {
    position: relative;
    transform: translate3d(-100%, 0, 0);
    visibility: visible;
  }
  /* right or prev direction */
  .carousel-item-prev.carousel-item-right
    + .carousel-item
    + .carousel-item
    + .carousel-item {
    position: relative;
    transform: translate3d(100%, 0, 0);
    visibility: visible;
    display: block;
    visibility: visible;
  }
}
/* LG */
@media (min-width: 991px) {
  /* show 4th item */
  .carousel-inner .active + .carousel-item + .carousel-item + .carousel-item {
    display: block;
  }
  .carousel-inner
    .carousel-item.active:not(.carousel-item-right):not(.carousel-item-left)
    + .carousel-item
    + .carousel-item
    + .carousel-item {
    transition: none;
  }
  /* Show 5th slide on lg if col-lg-3 */
  .carousel-inner
    .active.col-lg-3.carousel-item
    + .carousel-item
    + .carousel-item
    + .carousel-item
    + .carousel-item {
    position: absolute;
    top: 0;
    right: -25%; /*change this with javascript in the future*/
    z-index: -1;
    display: block;
    visibility: visible;
  }
  /* left or forward direction */
  .carousel-item-next.carousel-item-left
    + .carousel-item
    + .carousel-item
    + .carousel-item
    + .carousel-item {
    position: relative;
    transform: translate3d(-100%, 0, 0);
    visibility: visible;
  }
  /* right or prev direction //t - previous slide direction last item animation fix */
  .carousel-item-prev.carousel-item-right
    + .carousel-item
    + .carousel-item
    + .carousel-item
    + .carousel-item {
    position: relative;
    transform: translate3d(100%, 0, 0);
    visibility: visible;
    display: block;
    visibility: visible;
  }
}
</style>
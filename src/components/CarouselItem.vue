<template>
  <div
    :class="item.id === 1 ? 'carousel-item col-12 col-sm-6 col-md-4 col-lg-3 active' : 'carousel-item col-12 col-sm-6 col-md-4 col-lg-3'"
  >
    <div class="card">
      <a :href="item.imgSrc" target="_blank">
        <img :src="item.imgSrc" class="card-img-top" alt="..." />
      </a>
      <div class="card-body">
        <p class="card-text">{{item.description}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item"]
};
</script>
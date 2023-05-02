<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="before"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row mb-3 align-items-center"
      v-for="(item, index) in showItem"
      :key="index"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button
          class="btn btn-info text-white"
          v-on:click="$emit('add-item', item)"
        >
          +
        </button>
      </div>
      <div class="col-sm-4">
        <img :src="item.image" class="img-fluid d-block" :alt="item.name" />
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.name }}</h3>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-end">
          <price :value="Number(item.price)"></price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";
export default {
  name: "product-list",
  components: {
    Price,
  },
  props: ["products", "maximum"],
  computed: {
    showItem: function () {
      let max = this.maximum;
      return this.products.filter(function (item) {
        return Math.ceil(item.price) <= max;
      });
    },
  },
  methods: {
    before: function (el) {
      el.className = "d-none";
    },
    enter: function (el) {
      const delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeInRight";
      }, delay);
    },
    leave: function (el) {
      const delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeOutRight";
      }, delay);
    },
  },
};
</script>

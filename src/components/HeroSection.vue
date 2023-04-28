<template>
  <div class="hero">
    <div class="card-variants">
      <Card
          v-for="item in items"
          :key="item.id"
          :id="item.id"
          :img="item.img"
          :heading="item.heading"
          :author:="item.author"
          :salePrice="item.salePrice"
          :actualPrice="item.actualPrice"
          :buttonText="item.buttonText"
          :buttonState="getButtonState(item.id)"
          @addToCart="updateCartState(item.id)"
      />
    </div>
  </div>
</template>


<script>
import Card from './Card'

export default {
  name: "HeroSection",
  components: {
    Card,
  },
  props: {
    items: Array,
  },
  methods: {
    getButtonState(itemId) {
      const cardKey = `card-${itemId}`;
      const state = localStorage.getItem(cardKey);
      return state ? state : "default";
    },
    updateCartState(itemId) {
      const cardKey = `card-${itemId}`;
      localStorage.setItem(cardKey, "inCart");
    },
  },

};
</script>



<style scoped>
.no-results {
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 150%;
  color: #343030;
  margin-top: 20px;
}

h1 {
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 150%;
  color: #343030;
}
</style>

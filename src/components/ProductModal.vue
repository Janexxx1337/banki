<template>
  <a-modal
      :open="open"
      title="Описание"
      @ok="handleOk"
      @cancel="handleCancel"
      @update:open="handleOpenUpdate"
      centered
  >
      <div class="centered">
        <h2 v-if="item && Object.keys(item).length">{{ item.heading }}</h2>
        <p v-if="item && Object.keys(item).length">{{ item.description }}</p>
        <p v-if="item && Object.keys(item).length">Цена: {{ item.actualPrice }}</p>
      </div>
    <a-carousel class="carousel">
      <a-carousel-slide>
        <img src="/assets/1.png" />
      </a-carousel-slide>
      <a-carousel-slide>
        <img src="/assets/2.png" />
      </a-carousel-slide>
      <a-carousel-slide>
        <img src="/assets/3.png" />
      </a-carousel-slide>
      <a-carousel-slide>
        <img src="/assets/4.png" />
      </a-carousel-slide>
    </a-carousel>

  </a-modal>
</template>



<script>
import { Modal, Carousel } from 'ant-design-vue';
import { ref } from 'vue'

export default {
  components: {
    [Modal.name]: Modal,
    [Carousel.name]: Carousel,
    'a-carousel-slide': Carousel.Slide,
  },
  props: {
    item: {
      type: Object,
      default: () => ({}),
    },
    open: {
      type: Boolean,
      default: false,
    },
  },
  setup(props, { emit }) {
    const carouselRef = ref(null);

    const handleOk = () => {
      emit('close-modal');
    };

    const handleCancel = () => {
      emit('close-modal');
    };

    const handleOpenUpdate = (open) => {
      emit('update:open', open);
      if (open && carouselRef.value) {
        carouselRef.value.goTo(0);
      }
    };

    return {
      carouselRef,
      handleOk,
      handleCancel,
      handleOpenUpdate,
    };
  },
};
</script>

<style scoped>
img {
  margin: 0 auto;
}

.centered {
  text-align: center;
}
</style>

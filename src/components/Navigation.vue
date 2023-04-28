<template>
  <ul class="container">
    <li><a :style="{ color: color }" href="">Каталог</a></li>
    <li><a :style="{ color: color }" href="">Доставка</a></li>
    <li><a :style="{ color: color }" href="">Оплата</a></li>
    <li><a :style="{ color: color }" href="">Контакты</a></li>
    <li><a :style="{ color: color }" href="">О компании</a></li>
  </ul>
</template>

<script>
export default {
  name: 'NavigationModule',
  props: {
    color: {
      type: String,
      default: '#555555'
    }
  }
}
</script>

<style scoped>


.container {
  display: flex;
  gap: 48px;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 150%;
}

a {
  white-space: nowrap;
}

@media (max-width: 1440px) {
  .container {
    margin: 0;
  }
}

@media (max-width: 425px) {
  .container[data-v-40ab164b] {
    flex-wrap: wrap;
  }
  .container[data-v-61dd7a3d] {
    gap: 20px;
  }
}
</style>
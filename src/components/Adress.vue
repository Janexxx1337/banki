<template>
<div class="container">
 <div class="num">
   <img src="/assets/phone.svg" alt="phone">
   <a href="tel:78125555555">+7 (812) 555-55-55</a>
 </div>
<div class="address">
  <img src="/assets/adress-pin.svg" alt="">
  <p>г. Санкт-Петербург, ул. Ефимова, 3</p>
</div>
</div>
</template>

<script>
export default {
  name: "Address-module"
}
</script>

<style scoped>
.container {
  display: flex;
  align-items: center;
  margin-left: 126px;
  gap: 54px;
}

.address,.num {
  display: flex;
  gap: 8px;
}

a, p {
  font-weight: 400;
  font-size: 14px;
  color: #555555;
}

img {
  width: 14px;
  height: 14px;
}

</style>
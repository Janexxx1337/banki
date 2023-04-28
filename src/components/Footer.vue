<template>
  <footer>
    <div class="navigation">
      <NavigationModule/>
      <Address/>
    </div>
  </footer>
</template>

<script>
import NavigationModule from "@/components/Navigation";
import Address from "@/components/Adress";

export default {
  name: "Footer-module",
  components: {Address, NavigationModule}
}
</script>

<style scoped>
footer {
  margin-top: 312px;
  background: #ECEAEA;
}

.navigation {
  padding: 38px 0 38px 448px;
  display: flex;
}

 a {
  color: #555555;
}

 @media (max-width: 1440px) {
   .navigation {
     padding: 38px 0 38px 78px;
     flex-wrap: wrap;
     display: flex;
     flex-direction: column;
     gap: 30px;
   }
   .container {
     margin: 0;
   }
   footer {
     margin-top: 40px;
   }
 }

@media (max-width: 425px) {
  .navigation {
    padding: 38px 0 38px 15px;
  }
  .container {
    gap: 10px;
  }
}
</style>
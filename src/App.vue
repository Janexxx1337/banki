<template>
  <div class="wrapper">
    <Header />
    <div class="content">
      <HeroSection />
    </div>
    <Footer class="footer" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import HeroSection from "@/components/HeroSection";
import Footer from "@/components/Footer";

export default {
  name: "App",
  components: {
    Header,
    HeroSection,
    Footer,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Merriweather:wght@300;400;700&display=swap");

* {
  font-family: "Merriweather", serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  display: flex;
  flex-direction: column;
}

li {
  list-style-type: none;
}

a {
  text-decoration: none;
}

button {
  background: #403432;
  padding: 14px 36px;
  color: #fff;
  display: flex;
  justify-content: center;
  cursor: pointer;
}

.wrapper {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.content {
  flex: 1 0 auto;
}

.footer {
  flex: 0 0 auto;
}
</style>

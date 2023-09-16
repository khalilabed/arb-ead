<template>
  <header-page></header-page>
  <hero-section></hero-section>
  <div class="container py-5 titel-resp">
    <h3 class="pt-5 font-Bold">شاركنا الاحتفال واختار تصميمك بنفسك</h3>
    <p class="text-secondary font-Regular20">
      التصميم اللي بيناسب حسب ذوقك واحتياجك ب4 خطوات بسيطة
    </p>
  </div>
  <!-- <script-pages></script-pages> -->
  <!-- <select-choose></select-choose>
  <uplod-logo></uplod-logo>
  <preview-page></preview-page> -->
  <!-- <testig-page></testig-page> -->
  <!-- <canva-page></canva-page> -->
  <!-- <slider-test></slider-test> -->
  <script-pages></script-pages>
  <footer-page></footer-page>
</template>

<script>
import FooterPage from "./components/FooterPage.vue";
import HeaderPage from "./components/HeaderPage.vue";
import HeroSection from "./components/HeroSection.vue";
import ScriptPages from "./components/ScriptPages.vue";

export default {
  components: {
    HeaderPage,
    HeroSection,
    FooterPage,
    ScriptPages,
  },
};
</script>
<style scoped>
@import "@/assets/css/styles.css";
</style>
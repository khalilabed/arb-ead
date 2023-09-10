<template>
  <header-page></header-page>
  <hero-section></hero-section>
  <div class="container py-5">
    <h3 class="pt-5">شاركنا الاحتفال واختار تصميمك بنفسك</h3>
    <p class="text-secondary">
      التصميم اللي بيناسب حسب ذوقك واحتياجك ب4 خطوات بسيطة
    </p>
  </div>
  <!-- <script-pages></script-pages> -->
  <!-- <select-choose></select-choose>
  <uplod-logo></uplod-logo>
  <preview-page></preview-page> -->
  <testig-page></testig-page>
  <!-- <canva-page></canva-page> -->
  <footer-page></footer-page>
</template>

<script>
import FooterPage from "./components/FooterPage.vue";
import HeaderPage from "./components/HeaderPage.vue";
// import ScriptPages from "./components/ScriptPages.vue";
// import PreviewPage from "./components/PreviewPage.vue";
// import SelectChoose from "./components/SelectChoose.vue";
import HeroSection from "./components/HeroSection.vue";
import TestigPage from "./components/TestigPage.vue";
// import CanvaPage  from "./components/CanvaPage.vue";

// import UplodLogo from "./components/UplodLogo.vue";

export default {
  components: {
    HeaderPage,
    HeroSection,
    FooterPage,
    // CanvaPage
    TestigPage
    // UplodLogo,
    // PreviewPage,
    // SelectChoose,
    // ScriptPages,
  },
};
</script>
<style>
body {
  direction: rtl;
}

</style>
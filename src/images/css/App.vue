<template>
  <v-app>
    <navigation :color="color" :flat="flat" />
    <v-main class="pt-0">
      <home />
      <about />
      <download />
      <pricing />
      <contact />
    </v-main>
    <div class="div-bottons">
      <btn-section v-scroll="onScroll" />
    </div>
    <foote />
  </v-app>
</template>

<style scoped>
.v-main {
  background-image: url("~@/assets/img/bgMain.png");
  background-attachment: fixed;
  background-position: center;
  background-size: cover;
}

.div-bottons {
  z-index: 999;
  position: fixed;
  bottom: 10px;
  /* Puedes ajustar la posición vertical */
  right: 10px;
  /* Puedes ajustar la posición horizontal */
  padding: 10px;
  display: grid;
  grid-template-columns: repeat(2);
  grid-template-rows: repeat(2);
  gap: 3px;
}
</style>

<script>
import about from "./components/AboutSection";
import btnSection from "./components/BtnSection";
import BtnSection from './components/BtnSection.vue';
import contact from "./components/ContactSection";
import download from "./components/DownloadSection";
import foote from "./components/Footer";
import home from "./components/HomeSection";
import navigation from "./components/Navigation";
import pricing from "./components/PricingSection";


export default {
  name: "App",

  components: {
    navigation,
    foote,
    home,
    about,
    download,
    pricing,
    btnSection,
    contact,
    BtnSection,
  },

  data: () => ({
    fab: null,
    color: "",
    flat: null,
  }),

  created() {
    const top = window.pageYOffset || 0;
    if (top <= 60) {
      this.color = "transparent";
      this.flat = true;
    }
  },

  watch: {
    fab(value) {
      if (value) {
        this.color = "secondary";
        this.flat = false;
      } else {
        this.color = "transparent";
        this.flat = true;
      }
    },
  },

  methods: {
    onScroll(e) {
      if (typeof window === "undefined") return;
      const top = window.pageYOffset || e.target.scrollTop || 0;
      this.fab = top > 60;
    },
    toTop() {
      this.$vuetify.goTo(0);
    },
  },
};
</script>

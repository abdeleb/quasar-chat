<template>
  <q-layout view="hHh lpR fFr">
    <HeaderPage />
    <q-page-container>
      <router-view />
    </q-page-container>
    <FooterPage v-if="userGoogle" />
  </q-layout>
</template>

<script setup>
import HeaderPage from "../components/HeaderPage.vue";
import FooterPage from "../components/FooterPage.vue";
import { inject } from "vue";

const userGoogle = inject("userGoogle");

setTimeout(() => {
  window.scrollTo(0, document.body.scrollHeight);
}, 2000);
</script>

<template>
  <router-view v-if="userGoogle !== false" />
</template>

<script setup>
import { ref, provide } from "vue";
import { onAuthStateChanged } from "firebase/auth";
import { auth } from "./firebase";
import { useQuasar } from "quasar";

const $q = useQuasar();
$q.loading.show();

const userGoogle = ref(false);
provide("userGoogle", userGoogle);

onAuthStateChanged(auth, (user) => {
  //console.log(user);
  userGoogle.value = user;
  setTimeout(() => {
    $q.loading.hide();
  }, 1000);
});
</script>

<template>
  <q-header elevated class="bg-primary text-white">
    <q-toolbar>
      <q-toolbar-title>
        <q-avatar>
          <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg" />
        </q-avatar>
        Quasar Chat
      </q-toolbar-title>
      <q-btn
        label="Ingresar"
        color="secondary"
        @click="accesGoogle"
        v-if="!userGoogle"
      />
      <q-btn
        label="Salir"
        color="secondary"
        @click="logoutGoogle"
        v-if="userGoogle"
      />
    </q-toolbar>
  </q-header>
</template>

<script setup>
import { ref, inject } from "vue";
import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { auth } from "../firebase";

const userGoogle = inject("userGoogle");

const accesGoogle = () => {
  const provider = new GoogleAuthProvider();
  signInWithPopup(auth, provider).catch((e) => console.log(e));
};

const logoutGoogle = () => {
  signOut(auth).catch((e) => console.log(e));
};
</script>

<template>
  <q-footer elevated class="primary">
    <q-toolbar>
      <q-input
        class="full-width"
        dark
        label="Ingrese texto"
        v-model="text"
        @keyup.enter="addText"
      >
        <template v-slot:append>
          <q-icon
            name="send"
            class="cursor-pointer"
            typeof="submit"
            @click="addText"
          />
        </template>
      </q-input>
    </q-toolbar>
  </q-footer>
</template>

<script setup>
import { ref } from "vue";
import { collection, addDoc } from "firebase/firestore";
import { db, auth } from "../firebase";

const text = ref();
const addText = () => {
  addDoc(collection(db, "chats"), {
    text: text.value,
    uid: auth.currentUser.uid,
    time: Date.now(),
    displayName: auth.currentUser.displayName,
  })
    .then(() => {
      text.value = "";
      console.log("Aquí iría un sonido.");
    })
    .catch((e) => console.log(e));
  console.log(text.value);
};
</script>

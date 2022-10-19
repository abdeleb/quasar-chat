<template>
  <q-page v-if="!userGoogle">
    <p class="q-mt-xl text-center text-primary">Debes iniciar sesión.</p>
  </q-page>
  <q-page v-else>
    <div class="q-pa-md row justify-center">
      <div style="width: 100%; max-width: 400px">
        <template v-for="message in messages" :key="message.id">
          <q-chat-message
            :text="[message.text]"
            :sent="message.uid === auth.currentUser.uid"
            :name="message.displayName"
          />
        </template>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref, inject } from "vue";
import { collection, query, onSnapshot, orderBy } from "firebase/firestore";
import { db, auth } from "../firebase";

const userGoogle = inject("userGoogle");

const messages = ref([]);

const q = query(collection(db, "chats"), orderBy("time"));
const unsubscribe = onSnapshot(q, (snapshot) => {
  // if (userGoogle.value) {
  snapshot.docChanges().forEach((change) => {
    if (change.type === "added") {
      // console.log("New chat: ", change.doc.data());
      messages.value.push({
        id: change.doc.id,
        ...change.doc.data(),
      });
      setTimeout(() => {
        window.scrollTo(0, document.body.scrollHeight);
      }, 200);
    }
  });
  // }
});
</script>

<script setup lang="ts">
import { ref } from "vue";
const message = ref(null);

async function getMessage() {
  try {
    const response = await fetch("http://localhost:3030");
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const json = await response.json();
    message.value = json.message;
  } catch (error) {
    console.error("Error fetching message:", error);
    message.value = "Failed to fetch message.";
  }
}
</script>

<template>
  <h1>Rust + Vue</h1>
  <div v-if="message">Received: {{ message }}</div>
  <div v-else>No message</div>
  <button @click="getMessage()">Get Message</button>
</template>

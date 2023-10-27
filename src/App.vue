<template>
  <form class="form-container" @submit.prevent="onSubmit">
    <div class="form-control">
      <label class="form-label">Title</label>
      <input v-model="form.title" required class="form-input" type="text" />
    </div>

    <div class="form-control">
      <label class="form-label">Text</label>
      <textarea v-model="form.text" required class="form-textarea" rows="6"></textarea>
    </div>

    <button class="form-btn" type="submit">Send</button>
  </form>
</template>

<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";

const API_TOKEN = "6703981790:AAGhbkA412wRbs1FcbE4MUhg0JeMicVgTEo";

const form = ref({
  title: "",
  text: "",
});

const onSubmit = () => {
  const message = `<b>${form.value.title}</b>\n\n${form.value.text}`

  axios.post(`https://api.telegram.org/bot${API_TOKEN}/sendMessage`, {
    chat_id: "-1001933367047",
    text: message,
    parse_mode: "html"
  }).finally(() => {
    form.value.title = ""
    form.value.text = ""
  });
};
</script>

<script setup lang="ts">
import { supabase } from "../components/supabase"

const feedback = reactive({
  text: '',
  name: '',
  email: '',
})

const emit = defineEmits()

const insertFeedback = async () => {
  const { data, error } = await supabase
    .from('feedback_database')
    .insert([
      {
        name: feedback.name,
        email: feedback.email,
        text: feedback.text,
        id: 2
      }
    ])
  emit('close-popup-message')
}
</script>
<template>
  <div class="background_overlay">
    <div class="message">
      <div class="text-2xl w-full flex justify-end">
        <button @click="$emit('close-popup-message')">&#10006;</button>
      </div>
      <h3 class="text-3xl text-center pb-2">Give us feedback</h3>
      <hr class="bg-gray-500 h-0.5 mb-8">
      <textarea v-model="feedback.text" placeholder="Write your feedback" class="w-full textarea"></textarea>
      <div class="flex justify-center gap-14">
        <div class="flex flex-col gap-2 pt-4 w-full">
          <span>From:</span>
          <input type="text" v-model="feedback.name" class="w-full" placeholder="From">
        </div>
        <div class="flex flex-col gap-2 pt-4 w-full">
          <span>E-mail:</span>
          <input type="text" v-model="feedback.email" class="w-full" placeholder="E-mail">
        </div>
      </div>
      <div class="flex w-full justify-center pt-7">
        <button type="submit" @click="insertFeedback()"
          class="button bg-gradient-to-r from-cyan-500 to-blue-500 text-white w-20 p-1.5 rounded-sm">Submit</button>
      </div>
    </div>
  </div>
</template>
<style scoped>
.background_overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  background-color: #000000da;
}

.message {
  width: 620px;
  height: 700px;
  background-color: #ffffff;
  padding: 24px;
  border-radius: 8px;
  margin: auto;
}

.dark-mode .message {
  background-color: #1c1917;
}

.textarea {
  height: 380px;
  padding: 8px;
}

input,
textarea {
  border: 1px solid black;
  border-radius: 4px;
  padding: 4px;
}

.dark-mode textarea {
  background-color: #292524;
}
</style>
<script setup>
import { info } from '../components/content/info'

definePageMeta({
  middleware: 'auth'
})

const user = useSupabaseUser()
onBeforeMount(() => {
  if (!user.value) {
    navigateTo('/')
  }
})

useHead({
  title: 'Phisher | Admin Portal: Home'
})
</script>
<template>
  <h2 class="text-4xl pb-20">Home</h2>
  <div class="grid grid-cols-3 gap-10">
    <Card v-for="item in info" :key="item.heading" v-bind="item" />
  </div>
</template>
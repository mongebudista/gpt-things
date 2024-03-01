<template>
  <div>
    <h1>Image Generator</h1>
    <form @submit.prevent="handleSubmit()">
      <input type="text" v-model="text">
      <button type="submit">Go</button>
    </form>
        <a v-if="new_img" href={{ new_img }}>kkkk</a>
  </div>
</template>

<script setup>
import OpenAI from "openai"

const text = ref("")
const new_img = ref()

function handleSubmit() {
  main();
}

async function main() {
  const openai = new OpenAI({apiKey: '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',dangerouslyAllowBrowser: true})
  const completion = await openai.images.generate({
    size: '1024x1024',
    model: 'dall-e-3',
    prompt: text.value
  });

  new_img.value = completion.data[0].url
  console.log(completion.data[0].url)
}
</script>

<style scoped>
</style>
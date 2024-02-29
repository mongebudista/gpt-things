<template>
  <div>
    <div>
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/image">Image</NuxtLink>
    </div>
    <h1>Chat</h1>
    <p>Using ChatGPT 3.5-turbo</p>
    <form @submit.prevent="handleSubmit()">
      <input class="input" type="text" v-model="text" id="text">
      <button type="submit">Enviar</button>
    </form>
    <div class="response-box" v-if="gpt_response">
      {{ gpt_response }}
    </div>
  </div>
</template>

<script setup>
import OpenAI from "openai";

const text = ref("")
const gpt_response = ref("")

function handleSubmit() {
  main();
}

async function main() {
  const openai = new OpenAI({apiKey: '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',dangerouslyAllowBrowser: true})
  const completion = await openai.chat.completions.create({
    messages: [{ role: "system", content: text.value }],
    model: "gpt-3.5-turbo",
  });

  gpt_response.value = completion.choices[0].message.content
  console.log(completion.choices[0]);
}
</script>

<style scoped>
form {
  display: flex;
}
.input {
  width: 30rem;
  padding: 15px;
  font-size: 18px;
}

.response-box {
  font-size: 12px;
  line-height: 20px;
  max-width: 500px;
}

button {
  background-color: #30696b;
  color: white;
  border: 0;
  padding: 10px 15px;
  transition: all 0.3s ease-in;
  cursor: pointer;
}

button:hover {
  background-color: rgb(116, 43, 162);
}

p {
  font-size: 8px;
}

</style>

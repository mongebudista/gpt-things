<template>
  <div>
    <h1>CHAT</h1>
    <Card />
    <p>Using ChatGPT 3.5-turbo</p>
    <form @submit.prevent="handleSubmit()">
      <input class="input" type="text" v-model="text" id="text">
      <button type="submit">Enviar</button>
    </form>
    <div v-if="is_loading">
      <h1>GPT is thinking</h1>
    </div>
    <div class="response-box" v-else="gpt_response">
      <p class="typing">{{ gpt_response }}</p>
    </div>
  </div>
</template>

<script setup>
import OpenAI from "openai";

const text = ref("")
const is_loading = ref(false);
const gpt_response = ref("")

function handleSubmit() {
  main();
}

async function main() {
  is_loading.value = true;
  const openai = new OpenAI({apiKey: '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',dangerouslyAllowBrowser: true})
  const completion = await openai.chat.completions.create({
    messages: [{ role: "system", content: text.value, }],
    model: "gpt-3.5-turbo-16k",
  });
  gpt_response.value = completion.choices[0].message.content
  console.log(completion.choices[0]);

  is_loading.value = false;
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

form > button {
  max-width: 80px;

}

.input {
  width: 30rem;
  padding: 15px;
  font-size: 18px;
  margin: 10px 0;
}

.response-box {
  color: white;
}

.typing {
  overflow: hidden; /* Ensure the text is not visible until the typewriter effect*/
  font-size: 16px;
  white-space: nowrap; /* Keeps the text on a single line */
  animation: typing 2s steps(80) forwards;
}

/* The typing animation */
@keyframes typing {
  from { width: 0 }
  to { width: 100% }
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

h1 {
  font-size: 42px;
}
p {
  font-size: 12px;
  color: white;
}

</style>

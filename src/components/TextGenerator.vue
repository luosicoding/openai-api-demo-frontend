<script setup>
import axios from 'axios'
import { ref } from 'vue'

const promptForText = ref(null)
const generatedText = ref('')

async function generateText() {
  try {
    const response = await axios.post('http://localhost:4000/openai/text', {
      prompt: promptForText.value.value
    });
    generatedText.value = response.data.description
  } catch (error) {
    console.error(error)
  } 
}
</script>

<template>
  <div class="container">
    <h1 class="title">OpenAI文本生成器</h1>

    <p>请输入提示文字</p>
    <textarea class="prompt-box" ref="promptForText"></textarea>
    <input type="button" value="生成文字" class="text-generate-button" @click="generateText"/>
    <div class="generated-text">
      {{ generatedText }}
    </div>
  </div>
</template>

<style scoped>
.container {
  margin: auto;
  max-width: 800px;
  border-radius: 5px;
  text-align: center;
  background-color: beige;
}
.title {
  padding: 20px;
  text-align: center;
}
.prompt-box {
  margin: auto;
  width: 80%;
  height: 4em;
  padding: 2px;
  display: block;
}
.text-generate-button {
  margin-top: 10px;
  font-size: 20px;
}
.generated-text {
  overflow: hidden;
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px;
  background-color: #FFFFFF;
  width: 100%;
}
</style>

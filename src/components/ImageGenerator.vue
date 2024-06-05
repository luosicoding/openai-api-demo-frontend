<script setup>
import axios from 'axios'
import { ref } from 'vue'

defineProps({
  msg: String,
})

const prompt = ref(null)
const imageUrl = ref('')
const loading = ref(false)

async function generateImage() {
  try {
    loading.value = true
    const response = await axios.post('http://localhost:4000/openai/image', {
      prompt: prompt.value.value
    });
    imageUrl.value = response.data.imageUrl
  } catch (error) {
    console.error(error)
  } finally {
    loading.value = false
  }
}
</script>

<template>
  <div class="container">
    <h1 class="title">OpenAI图片生成器</h1>  
  
    <p>请输入提示文字</p>
    <textarea class="prompt-box" ref="prompt"></textarea>
    <input type="button" value="生成图片" class="image-generate-button" @click="generateImage"/>
    <div v-if="loading" class="help-text">正在生成图片...</div>
    <img v-if="!loading && imageUrl !== ''" :src="imageUrl" class="img"/>
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
.image-generate-button {
  margin-top: 10px;
  margin-bottom: 10px;
  font-size: 20px;
}
.help-text {
  margin-top: 10px;
}
.img {
  margin-top: 10px;
  width: 400px;
  height: 400px;
}
</style>

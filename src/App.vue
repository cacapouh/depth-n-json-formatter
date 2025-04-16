<script setup lang="ts">
import { computed, ref } from 'vue'
import { jsonfmt } from '@/jsonfmtjs.js'

const depth = ref(1)
const jsonString = ref(
  '{"min_position":8,"has_more_items":false,"items_html":"Bike","new_latent_count":1,"data":{"length":20,"text":"Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."},"numericalArray":[23,32,20,31,30],"StringArray":["Carbon","Oxygen","Oxygen","Nitrogen"],"multipleTypesArray":true,"objArray":[{"class":"lower","age":5},{"class":"middle","age":7},{"class":"upper","age":5},{"class":"upper","age":8},{"class":"upper","age":4}]}',
)

const incrementDepth = () => {
  depth.value = depth.value + 1
}
const decrementDepth = () => {
  if (0 <= depth.value - 1) depth.value = depth.value - 1
}

const formattedJson = computed(() => {
  try {
    return jsonfmt(jsonString.value, depth.value, 2)
  } catch (e) {
    console.error(e)
    return 'Failed to format json'
  }
})
</script>

<template>
  <div class="container">
    <h1>Depth-N JSON Formatter</h1>

    <label>Depth:&nbsp;</label>
    <button @click="decrementDepth">&lt;</button>
    {{ depth }}
    <button @click="incrementDepth">&gt;</button>
    <br />

    <label>Input:</label>
    <br />
    <textarea v-model="jsonString" class="textarea"></textarea>
    <br />

    <label>Output:</label>
    <br />
    <textarea readonly :value="formattedJson" class="textarea"></textarea>
  </div>
</template>

<style>
.container {
  width: 960px;
  margin-inline: auto;
}

.textarea {
  width: 100%;
  min-height: 200px;
}
</style>

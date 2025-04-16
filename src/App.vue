<script setup lang="ts">
import { computed, ref } from 'vue'

const depth = ref(1)
const jsonString = ref(
  '{"glossary":{"title":"example glossary","GlossDiv":{"title":"S","GlossList":{"GlossEntry":{"ID":"SGML","SortAs":"SGML","GlossTerm":"Standard Generalized Markup Language","Acronym":"SGML","Abbrev":"ISO 8879:1986","GlossDef":{"para":"A meta-markup language, used to create markup languages such as DocBook.","GlossSeeAlso":["GML","XML"]},"GlossSee":"markup"}}}}}',
)

const incrementDepth = () => {
  depth.value = depth.value + 1
}
const decrementDepth = () => {
  if (0 <= depth.value - 1) depth.value = depth.value - 1
}

const formattedJson = computed(() => {
  return jsonString.value
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

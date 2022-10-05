<script setup lang="ts">
import { Repl, ReplStore } from '@vue/repl';
import { ref, version } from 'vue';
import '@vue/repl/style.css';

const store = new ReplStore({
  defaultVueRuntimeURL: `https://unpkg.com/vue@${version}/dist/vue.esm-browser.js`,
});

const files: Record<string, string> = {};
const defaultMainFile = 'index.html';
const mainCode = `
<div id="app">
  <h1>{{ msg }}</h1>
  <input v-model="msg"/>
</div>

<script type="module">
import { createApp, ref } from 'vue';

createApp({
  setup() {
    const msg = ref('Hello word')

    return {
      msg
    }
  }
}).mount('#app')
<\/script>
`.trim();

files[defaultMainFile] = mainCode;
files['style.css'] = `
h1 {
  color: red
}
`.trim();

store.setFiles(files, defaultMainFile);
</script>

<template>
  <Repl
    layout="vertical"
    :store="store"
    :showImportMap="true"
    :showCompileOutput="false"
    :clearConsole="false"
  />
</template>

<style scoped></style>

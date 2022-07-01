<template>
  <img
      alt="Vue logo"
      src="./assets/logo.png"
      @click="chColor"
  />
  <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" />
</template>

<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { DEFAULT_COLOR } from './customization/default'
import custom from './customization/custom'
import { computed } from '@vue/runtime-core'
import {ref} from "vue";

const customColor = ref(custom.main)

function chColor () {
  if (customColor.value == 'green') {
    customColor.value = custom.main;
  } else {
    customColor.value = 'green';
  }

}

const color = computed(() => custom.main ?? DEFAULT_COLOR.SECONDARY)
const anotherColor = computed(() => customColor.value ?? DEFAULT_COLOR.SECONDARY)

</script>


<style>
* {
  --color: v-bind(color);
  --another-color: v-bind(anotherColor);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

a {
  color: var(--linksColor)
}
</style>

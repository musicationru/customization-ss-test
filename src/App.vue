<template>
  <div
      id="wrap"
  >
    <img
        alt="Vue logo"
        src="./assets/logo.png"
        @click="chColor"
    />
    <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" />
  </div>
</template>

<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { DEFAULT_COLORS } from './customization/default'
import custom from './customization/custom'
import {ref, computed} from "vue";

const customColor = ref(custom.secondary)

function chColor () {
  if (customColor.value == 'black') {
    customColor.value = custom.error;
  } else {
    customColor.value = 'black';
  }
}


const color = computed(() => custom.main ?? DEFAULT_COLORS.MAIN)
const anotherColor = computed(() => customColor.value ?? DEFAULT_COLORS.SECONDARY)

// async function returning color
const getColor = async (): Promise<string> => {
  return new Promise((resolve, reject) => {
    setTimeout(
    () => resolve('#34fa56'),
    5000
    )
  })
}

// async updating color
(async () => {
  customColor.value = await getColor();
})();

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
  color: var(--another-color)
}
</style>

<script setup>
import { computed, ref } from 'vue';

const ourWord = ref('')

const letters = computed(() => {
  return ourWord.value.split('')
})

function letterScore(l) {
  if (!l) {
    return -1
  }
  return l.toLowerCase().charCodeAt(0) - 96
}

const wordScore = computed(() => {
  if (!letters.value) {
    return
  }

  let s = 0
  for (let i = 0; i < letters.value.length; i++) {
    s += letterScore(letters.value[i])
  }
  return s
})
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>Dollar Words</h1>
      <input v-model="ourWord" placeholder="enter a word">
      <br>
      <br>
      <h3>Break it up into letters</h3>
      {{ letters }}
      <br>
      <br>
      <h3>Get the amount for each letter</h3>
      <p v-for="l in letters">
        {{ l }} - {{ letterScore(l) }}
      </p>
      <br>
      <h3>Add it up!</h3>
      <p>{{ ourWord }} - {{ wordScore }}</p>
    </div>
  </header>

  <main>
  </main>
</template>

<style scoped>
</style>

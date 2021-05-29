<template>
<div class="app">
  <h1>Markdown App</h1>
</div>
  <section>
    <article>
      <textarea :value="text" @input="update"></textarea>
    </article>
    <article v-html="markedText"></article>
  </section>
</template>

<script>
import { computed, ref } from 'vue'
import marked from 'marked'

export default {
  name: 'Markdown',
  props: {},
  setup() {
    const text = ref('')
    const timeout = ref('')

    const markedText = computed(() => {
      return marked(text.value)
    })

    const update = (e) => {
      const task = () => (text.value = e.target.value)
      debounce(task, 500)
    }

    function debounce(func, wait = 1000) {
      clearTimeout(timeout.value)
      timeout.value = setTimeout(func, wait)
    }

    return { text, markedText, update}
  }
}
</script>

<style scoped>
.app {
  width: fit-content;
  margin: auto;
}
section {
  display: grid;
  grid-template-columns: 1fr 1fr ;
  grid-template-rows: 90vh; 
  grid-gap: 10px;
}

article {
  background: lightgray;
  border: 1px solid black;
}

textarea {
  width: 100%;
  height: 100%;
}
</style>

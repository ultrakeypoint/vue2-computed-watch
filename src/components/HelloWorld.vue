<template>
  <div>
    <h1 v-bind="$attrs">Hello world</h1>
    <span v-if="showMessage">Now you see me {{ showMessage }}</span>

    <br />
    <button @click="download">set loading</button>

    loading: {{ loading }}
    <div v-for="element in array">
      {{ element }}
    </div>
  </div>
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    showMessage: { type: Boolean, required: true, default: false },
  },
  model: {
    x: 1,
  },
  data() {
    return {
      loading: false,
      array: [1, 2, 3],
      id: Math.random()
    }
  },
  methods: {
    download() {
      this.loading = !this.loading
    },
    click() {
      console.log('test' + this.id);
    }
  },
  mounted() {
    window.addEventListener('click', this.click)
  },
}
</script>

<template>
  <div id="example">
    <p>Original message: "{{ message }}"</p>
    <p>Computed message: "{{ requestMessage }}"</p>
    <p>watched message: "{{ watchedMessage }}"</p>

    <button @click="update()">update</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      updatecount: 0,
      message: '뭐 먹을까요?',
      watchedMessage: '',
      loading: false,
    }
  },

  computed: {
    requestMessage: function () {
      return '점심 ' + this.message
    },
  },

  watch: {
    requestMessage: async function (n, o) {
      this.loading = true
      const r = await this.resolveAfter2seconds(2)
      this.watchedMessage = n + ++this.updatecount
      this.loading = false
    },
  },

  methods: {
    async update() {
      this.requestMessage = this.requestMessage + '(' + Math.random() + ')'
    },
    resolveAfter2seconds(x) {
      console.log('resolveAfter10second')
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(' - 밥' + this.updatecount)
        }, 2000)
      })
    },
  },
}
</script>

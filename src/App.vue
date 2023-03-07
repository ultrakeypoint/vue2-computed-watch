<template>
  <div id="example">
    <p>updatecount: "{{ updatecount }}"</p>
    <p>Original message: "{{ message }}"</p>
    <p>Computed reversed message: "{{ reversedMessage }}"</p>
    <p>Computed reversed message: "{{ this.message.split('').reverse().join('') }}"</p>
    <p>Computed reversed watched: "{{ watched }}"</p>
    <p>Computed reversed message: "{{ this.test() }}"</p>
    <p>Computed reversed message: "{{ this.test() }}"</p>
    <p>Computed reversed message: "{{ this.test() }}"</p>

    <button @click="update()">update</button>

    <div>{{ getSelectList() }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      updatecount: 0,
      message: '오늘은 무엇을 먹을까요?',
      watched: '',
    }
  },
  
  computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    },
    // reversedMessage: async function () {
    //   this.variable = '1234'
    //   const r = await this.resolveAfter2seconds(2)
    //   return this.message.split('').reverse().join('')
    // },
  },

  watch: {
    reversedMessage: async function (n, o) {
      const r = await this.resolveAfter2seconds(2)
      this.watched = n + r
    },
  },

  methods: {
    async update() {
      this.message = this.message + ++this.updatecount
    },
    resolveAfter2seconds(x) {
      console.log('resolveAfter10second')
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(' - 생각중' + this.updatecount)
        }, 2000)
      })
    },
    test() {
      console.log(1)
      return 1
    },
    getSelectList() {
      this.variable = 'test'
      return [1, 2, 3, 4, 5]
    },
  },
}
</script>

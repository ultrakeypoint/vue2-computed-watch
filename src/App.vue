<template>
  <div id="example">
    <p>updatecount: "{{ updatecount }}"</p>
    <p>Original message: "{{ message }}"</p>
    <p>Computed reversed message: "{{ reversedMessage }}"</p>
    <p>Computed reversed message: "{{ this.message.split('').reverse().join('') }}"</p>
    <p>Computed reversed watched: "{{ watched }}"</p>

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
      message2: '2',
      message3: '3',
      watched: '',
    }
  },

  computed: {
    // reversedMessage: function () {
    //   ㅁㄴㅇㄹ
    //   return this.message.split('').reverse().join('')
    // },
    // reversedMessage: async function () {
    //   this.variable = '1234'
    //   const r = await this.resolveAfter2seconds(2)
    //   return this.message.split('').reverse().join('')
    // },
    // reversedMessage: function () {
    //   // this.resolveAfter2seconds(2)

    //   // 1
    //   // 2
    //   // 3

    //   return this.message.split('').reverse().join('')
    // },
    reversedMessage: function () {
      // this.message = '1'
      // this.message2 = '2'
      this.message = this.message3

      return this.message2 + this.message
    },
  },

  watch: {
    reversedMessage: function (n, o) {
      const r = this.resolveAfter2seconds(2)
      this.watched = n + r
    },
  },

  methods: {
    async update() {
      // this.message = this.message + ++this.updatecount
      this.message3 = this.message3 + '1'
    },
    resolveAfter2seconds(x) {
      console.log('resolveAfter10second')
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(' - 생각중' + this.updatecount)
        }, 2000)
      })
    },

    // selectlist 가져오는 거다.
    // getSelectList
    getSelectList() {
      this.variable = 'test'
      //
      return [1, 2, 3, 4, 5]
    },
  },
}
</script>

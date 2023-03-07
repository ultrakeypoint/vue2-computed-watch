<template>
  <div id="example">
    <p>updatecount: "{{ updatecount }}"</p>
    <p>Original message: "{{ message }}"</p>
    <p>Computed reversed message: "{{ reversedMessage }}"</p>
    <p>Computed reversed watched: "{{ loadingWatch }}"</p>

    <button @click="update()">update</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      updatecount: 0,
      message: '오늘은 무엇을 먹을까요?',
      watchedMessage: '',

      myMoney: 0,
      debt: 0,

      loading: false,
    }
  },

  computed: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    },
    loadingWatch: function () {
      return this.loading ? '생각중' : this.watchedMessage
    },
  },

  watch: {
    reversedMessage: async function (n, o) {
      this.loading = true
      const r = await this.resolveAfter2seconds(2)
      this.watchedMessage = n + ++this.updatecount + r
      this.loading = false
    },
  },

  methods: {
    async update() {
      this.message = this.message + '?'
    },
    resolveAfter2seconds(x) {
      console.log('resolveAfter10second')
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(' - 밥' + this.updatecount)
        }, 2000)
      })
    },

    // selectlist 가져오는 거다.
    // getSelectList
    increaseDebt(money) {
      this.debt = money
    },
    getMyMoney() {
      // this.myDebt = this.myDebt + 100
      return this.myMoney
    },
  },
}
</script>

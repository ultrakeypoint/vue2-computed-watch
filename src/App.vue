<template>
  <div>
    <p>Query: "{{ eating }}"</p>
    <p>Result: "{{ behaviorMessage }}"</p>
    <button @click="eat(10)">1. heavy 간식 먹기</button>
    <button @click="eat(2)">2. 물 먹기</button>
    <div>(한번에 1개의 음식만 먹을 수 있기 때문에 heavy 간식을 먹는 중에는 물을 먹을 수가 없다.)</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: '',
      behaviorMessage: '',
      isEating: false,
      eatSize: 0,
      eatCount: 0,
    }
  },

  computed: {
    eating: function () {
      return this.message ? this.message + '!' : '무엇을 먹을까요?'
    },
  },

  watch: {
    eating: async function (n) {
      this.isEating = true
      this.behaviorMessage = this.eatSize + `칼로리 먹는 즁... 예상시간: ${this.eatSize}초`
      const r = await this.resolveEating(this.eatSize)
      this.behaviorMessage = r
      this.isEating = false
    },
  },

  methods: {
    async eat(size) {
      if (this.isEating) {
        alert('먹는중입니다...')
        return
      }
      this.eatSize = 0
      this.message = ''
      this.message = size + `칼로리를 ${++this.eatCount}번째 먹겠습니다.`
      this.eatSize = size
    },
    resolveEating(time) {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve('다 머것당')
        }, time * 1000)
      })
    },
  },
}
</script>

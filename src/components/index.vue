<template>
  <div>
    <kcp-input v-model="input" :disabled="false">
      <template slot="prepend">
        123123
      </template>
      <template slot="append">
        123123
      </template>
    </kcp-input>
    <button @click="test">按钮</button>
  </div>
</template>

<script>
import kcpInput from './input/input'

export default {
  data () {
    return {
      input: '测试一下'
    }
  },
  components: {
    kcpInput
  },
  methods: {
    test () {
      console.log(this.input)
    }
  }
}
</script>

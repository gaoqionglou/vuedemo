<template>
    <div>
        <p v-text="msg"></p>
        <button @click="handleClick">测试emit</button>
    </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'this is component A',
      eventParam: '-- this is eventParam --'
    }
  },
  methods: {
    handleClick () {
      this.$emit('myevent', this.eventParam)
    }
  }
}
</script>
<style scoped>

</style>

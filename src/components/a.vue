<template>
    <div>
      <!--my-value 在{{}}中要转换 -->
        <p>{{msg}}, and {{myValue}}</p>
        <button @click="handleClick">测试emit</button>
        <br>
        <slot name="header">no header</slot>
        <p>default content</p>
        <slot name="footer">no footer</slot>
    </div>
</template>

<script>
export default {
  props: {
    'data': String,
    'my-value': [String, Number]
  },
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

<template lang='pug'>
  div
    h1.m-4
      | {{ msg }}
</template>

<script>
  export default {
    name: 'Hello',
    data () {
      return {
        msg: 'Welcome to Github Fast Look'
      }
    }
  }
</script>
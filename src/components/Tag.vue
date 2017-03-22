<template lang="html">
  <li>{{tag[0]}}<span>{{tag[1]}}</span></li>
</template>

<script>
export default {
  props: ['tag']
}
</script>

<style lang="css">
li {
  display: inline-block;
  padding: 5px;
}

li span {
  display: block;
}
</style>

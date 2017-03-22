<template lang="html">
  <li v-on:click="filterTag(tag[0])">{{tag[0]}}<span>{{tag[1]}}</span></li>
</template>

<script>
export default {
  props: ['tag'],
  methods: {
    filterTag (tag) {
      console.log(tag, 'clicked')
      this.$emit('filterTag', tag)
    }
  }
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

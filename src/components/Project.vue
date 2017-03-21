<template lang="html">
  <div class="tile">
    <article  class="tile is-child box">
      <p class="title is-3" @click="linkClick(repo.html_url)">{{repo.name}}</p>
      <p class="subtitle">{{repo.description}}</p>
    </article>
  </div>
</template>

<script>
export default {
  name: 'project',
  props: ['repo'],
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    linkClick (url) {
      return window.open(url, '_blank')
    }
  }
}
</script>

<style lang="css">

article {

}

.title.is-3 {
  text-decoration: underline;
}

.title.is-3:hover {
  color: #EEEEEE;
  cursor: pointer;
}
</style>

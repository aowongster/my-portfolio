<template lang="html">
  <div class="tile is-ancestor">
    <div class="tile is-parent is-vertical">
      <template v-for="(repo, index) in repoData">
        <project :repo="repo"></project>
      </template>
    </div>
  </div>
</div>

</template>

<script>

import axios from 'axios'
import Project from './Project'

export default {
  name: 'project-list',
  components: {
    Project
  },
  data () {
    return {
      username: 'your username',
      repoData: []
    }
  },
  mounted () {
    this.getRepos('aowongster')
  },
  methods: {
    getRepos (username) {
      return axios.get(`https://api.github.com/users/${username}/repos`)
        .then(function (response) {
          // console.log(response.data)
          this.repoData = response.data.sort(function (a, b) {
            return new Date(b.updated_at) - new Date(a.updated_at)
          })
          // todo sort this
        }.bind(this))
    }
  }
}
</script>

<style lang="css">
</style>

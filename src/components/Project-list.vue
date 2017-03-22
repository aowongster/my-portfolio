<template lang="html">
  <div class="tile is-ancestor">

    <div class="tile is-parent is-vertical">
      <div class="tile is-child box">
        <ul>
        <template v-for="(count, key) in tags">
          <li>{{key}}:{{count}}</li>
        </template>
        </ul>
      </div>
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
  computed: {
    tags () {
      let tagDict = {}
      for (let i = 0; i < this.repoData.length; i++) {
        let lang = this.repoData[i].language
        if (lang) {
          tagDict[lang] = tagDict[lang] + 1 || 1
        }
      }
      console.log(tagDict)
      return tagDict
    }
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

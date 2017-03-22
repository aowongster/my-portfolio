<template lang="html">
  <div class="tile is-ancestor">

    <div class="tile is-parent is-vertical">
      <div class="tile is-child box">
        <ul>
        <template v-for="(tag, index) in tags">
          <tag :tag="tag" v-on:filterTag="filterRepos"></tag>
        </template>
        </ul>
      </div>
      <template v-for="(repo, index) in displayData">
        <project :repo="repo"></project>
      </template>
    </div>
  </div>
</div>

</template>

<script>

import axios from 'axios'
import Project from './Project'
import Tag from './Tag'

export default {
  name: 'project-list',
  components: {
    Project,
    Tag
  },
  data () {
    return {
      username: 'your username',
      repoData: [],
      displayData: []
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
      // console.log(tagDict)
      // change dict to array
      let tagArray = Object.keys(tagDict).map((key) => {
        return [key, tagDict[key]]
      })

      // sorting by second element
      tagArray.sort((first, second) => {
        return second[1] - first[1]
      })

      return tagArray
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

          this.displayData = this.repoData.slice() // copy array by val
          // todo sort this
        }.bind(this))
    },
    // filter and pass tags to website
    filterRepos (tag) {
      this.displayData = this.repoData.filter((repo) => {
        return repo.language === tag
      })
    }
  }
}
</script>

<style lang="css">

</style>

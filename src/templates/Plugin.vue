<template>
  <Layout :footer="false">
    <div class="plugins container flex flex-align-top" style="position: relative;">

          <div class="plugin-post__content mb" v-if="hit" v-html="content" />

        </template>
        <template v-else>
          <div class="plugins-intro container-sm post">
            <Connect />
            <div class="plugins-intro__text">
              <h1>Safe and useful cPanel code snippets</h1>
              <p class="lead">Useful commands and opensource scripts for cPanel. <span class="hide-for-small">Save your time and money with ready-to-use solutions and grow your business faster! ⚡️</span></p>

              <p>Visit our <g-link to="/docs/how-to-create-a-plugin">WordPress.org profile</g-link></p>
            </div>
          </div>
        </template>
      </Section>
     </div>
  </Layout>
</template>

<script>
import markdown from '../utils/markdown'
import algoliasearch from 'algoliasearch/lite'
import GitLabLogo from '~/assets/images/gitlab.svg'
import GitHubLogo from '~/assets/images/github-logo.svg'
import BitbucketLogo from '~/assets/images/bitbucket.svg'
import Connect from '~/components/Connect.vue'

import {
  createInstantSearch,
  AisInstantSearchSsr,
  AisStateResults,
  AisInfiniteHits,
  AisHighlight,
  AisConfigure,
  AisSearchBox,
  AisPoweredBy
} from 'vue-instantsearch'

const searchClient = algoliasearch(
  'OFCNCOG2CU',
  'e0925566b9cfa7d0d21586a0b365d78c'
)

const { instantsearch, rootMixin } = createInstantSearch({
  indexName: 'npm-search',
  searchClient
})

export default {
  components: {
    Connect,
    AisPoweredBy,
    AisSearchBox,
    AisConfigure,
    AisHighlight,
    AisInfiniteHits,
    AisStateResults,
    AisInstantSearchSsr
  },

  mixins: [rootMixin],

  data () {
    return {
      hit: null,
      hitsPerPage: 50,
      filters: 'keywords:gridsome-plugin AND deprecated:false'
    }
  },

  serverPrefetch () {
    return instantsearch.findResultsState({
      hitsPerPage: this.hitsPerPage,
      filters: this.filters
    })
  },

  computed: {
    isSingle () {
      return Boolean(this.$route.params.id)
    },

    owners () {
      return this.hit
        ? this.hit.owners.map(owner => {
            if (owner.name === 'hjvedvik') {
              return {
                ...owner,
                name: 'gridsome',
                link: 'https://www.npmjs.com/org/gridsome',
                avatar: 'https://avatars0.githubusercontent.com/u/17981963?s=200&v=4'
              }
            }

            return owner
          })
        : []
    },

    content () {
      return this.hit && this.hit.readme
        ? markdown(this.hit.readme)
        : ''
    }
  },

  watch: {
    $route: {
      handler: 'fetchCurrent',
      immediate: true
    }
  },

  metaInfo () {
    const meta = {
      title: 'Plugins',
      meta: []
    }

    if (this.hit) {
      meta.title = this.hit.name

      if (this.hit.description) {
        meta.meta.push({
          key: 'description',
          name: 'description',
          content: this.hit.description
        })
      }
    }

    return meta
  },

  methods: {
    async fetchCurrent () {
      if (!this.isSingle) {
        return
      }

      const { id: name } = this.$route.params
      const { results: [results] } = await searchClient.search([{
        indexName: 'npm-search',
        query: name
      }])

      this.hit = results.hits.find(hit => hit.name === name)
    },

    hitClasses (hit) {
      return {
        'plugin--active': this.hit && this.hit.name === hit.name
      }
    },

    repositoryIcon (repository) {
      switch (repository.host) {
        case 'github.com': GitHubLogo; break
        case 'gitlab.com': GitLabLogo; break
        case 'bitbucket.com': BitbucketLogo; break
      }

      return GitHubLogo
    }
  }
}
</script>

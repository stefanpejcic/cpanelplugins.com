<template>
  <Starters>
    <h1>Professional plugins for cPanel and WHM</h1>
    <p class="mb-x2">Our products are easy to set up, compatible with older WHM versions and very easy to use. What is more, the modules can be combined in order to provide your customers with interesting product bundles like for example a VPS with additional cPanel plugins.</p>

    <div class="grid-cols grid-cols--3 mb">
      <StarterCard v-for="starter in $page.defaultStarters.edges" :key="starter.node.id" :node="starter.node"  />
    </div>

    <hr />

    <h3>Recent</h3>
    <div class="grid-cols grid-cols--3">
      <StarterCard v-for="starter in $page.starters.edges" :key="starter.node.id" :node="starter.node"  />
    </div>
  </Starters>
</template>

<script>
import Starters from '~/layouts/Starters.vue'
import StarterCard from '~/components/StarterCard.vue'

export default {
  components: {
    Starters,
    StarterCard
  },
  metaInfo: {
    title: 'Starters'
  }
}
</script>

<page-query>
query {
  defaultStarters: allStarter (
    sort: [{ by: "index", order: ASC }]
    filter: {
      featured: {
        eq: true
      }
    }
  ) {
    edges {
      node {
        id
        title
        path
        description
        preview
        repo
        platforms {
          title
          logo
        }
        author {
          title
          path
        }
      }
    }
  },
  starters: allStarter (
    sortBy: "index"
    order: DESC
    filter: {
      featured: {
        ne: true
      }
    }
  ) {
    edges {
      node {
        id
        title
        description
        preview
        repo
        path
        screenshot  (width: 840, height:840)
        platforms {
          title
          logo
        }
        author {
          title
          path
        }
      }
    }
  }
}
</page-query>



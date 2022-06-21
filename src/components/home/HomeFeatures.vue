<template>
  <Section dots="true">
    <div class="homepage-features grid-cols">

      <Feature>
        <h3>Easy to customize</h3>
        <p>All plugins can easily be White-labeled <br class="hide-for-small" /> Adding your logo is as simple as editing a single <strong>.php</strong> file.
        </p>
      </Feature>

      <Feature>
        <h3>OpenSource</h3>
        <p>All code is 100% open-source and can be included in your products.
        </p>
      </Feature>

      <Feature>
        <h3>Fast Support</h3>
         <p>We offer support regarding plugin functioning with all default cPanel Templates such as Jupiter and PaperLatern.
          </p>
      </Feature>

      <Feature>
        <h3>Always free</h3>
        <p>All plugins listed on CpanelPlugins are FREE to use and redistribute.</p>
      </Feature>


      <Feature>
        <h3>Clean code</h3>
        <p>We follow both best PHP coding practises and cPanel developer guidelines.
        </p>
      </Feature>

      <Feature>
        <h3>Well documented</h3>
        <p>We do our best to keep the docs always updated!</p>
      </Feature>

    </div>

  </Section>
</template>

<script>
import VueLogo from '~/assets/images/vue-logo.svg'
import GraphQlLogo from '~/assets/images/graphql-logo.svg'
export default {
  props: ['icon'],
  components: {
    VueLogo,
    GraphQlLogo,
  },
  computed: {
    iconClasses() {
      let classes = []
      return classes
    }
  }
}
</script>

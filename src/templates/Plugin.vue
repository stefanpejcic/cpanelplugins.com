<template>
  <Plugins class="plugin">
      <div class="plugin__header flex">
        <g-image class="plugin__header-platform-logo" v-if="$page.plugin.platforms" :src="$page.plugin.platforms.logo" />

        <strong class="plugin__header-title">{{ $page.plugin.title }}</strong>

        <div class="flex gap-20 hide-for-small" style="margin-left: auto">
          <a
            rel="noopener noreferrer"
            target="_blank"
            :href="githubUrl"
            title="View on GitHub"
            aria-label="View on GitHub"
            class="button button--blank">
            <github-icon />
          </a>
          <a
            rel="noopener noreferrer"
            target="_blank"
            v-if="$page.plugin.preview"
            :href="$page.plugin.preview"
            title="Live preview"
            aria-label="Live preview"
            class="button button--blank">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-eye"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path><circle cx="12" cy="12" r="3"></circle></svg>
          </a>

          <Popover name="InstallThis" :closeOnContentClick="false">
            <div slot="face">
              <button class="button primary button">Install now  </button>
            </div>

            <div slot="content">
              <p style="margin-bottom: .5rem; display: block;">
              To install this cPanel plugin you need to have <strong><g-link to="https://support.cpanel.net/hc/en-us/articles/360051754554-How-do-I-log-in-to-my-cPanel-account-as-root-">root</g-link></strong> account
              </p>
              <div class="mb">
                <code class="plugin__command flex" style="overflow: hidden;">
                  <span ref="command">
				  git clone https://github.com/{{ $page.plugin.repo }}.git
				  </span>
                  <button class="button button--xsmall" @click="copyCommand()">
                    <ClipboardIcon title="Copy to clipboard" width="16" height="16" />
                    <span style="margin-left: 0"> Copy </span>
                  </button>
                </code>
              </div>
              <hr />
              <!--div class="deploy-buttons flex">
                <a class="button button--small" style="width: 100%; text-align: center; display:block;" href="/plugin-installation">
                  <cPanelLogo alt="cPanel plugin installation service" height="16" /> cPanel plugin installation service - $9.95
                </a>
              </div-->
            </div>
          </Popover>
        </div>
      </div>


      <div class="plugin__image" style="order:2" v-if="$page.plugin.screenshot">
        <g-image :src="$page.plugin.screenshot" />
      </div>
      <hr v-else />

      <div class="plugin__content">

        <div style="width: 80%;" v-if="isLoading">
          <Skeleton />
          <Skeleton style="height: 15px" />
          <Skeleton style="height: 15px; width: 80%; opacity: .6;" />
          <Skeleton style="height: 15px; width: 85%; opacity: 1;"  />
          <Skeleton style="height: 15px; width: 85%; opacity: 1;"  />
          <Skeleton style="height: 15px; width: 65%; opacity: 1;"  />
          <Skeleton style="height: 15px; width: 55%; opacity: 1;"  />
          <Skeleton style="height: 15px; width: 75%; opacity: 1;"  />
        </div>

        <div v-html="readme" />
      </div>
  </Plugins>
</template>

<script>
import clipboard from 'clipboard-copy'
import markdown from '../utils/markdown'
import Plugins from '~/layouts/Plugins.vue'
import Skeleton from '~/components/Skeleton.vue'
import ClipboardIcon from '~/assets/images/icon-clipboard.svg'
import GithubIcon from '~/assets/images/github-logo.svg'
import cPanelLogo from '~/assets/images/cp_orange.svg'
import Popover from 'vue-popover'

const cache = {}

export default {
  components: {
    Plugins,
    Skeleton,
    ClipboardIcon,
    cPanelLogo,
    Popover,
    GithubIcon
  },

  data () {
    return {
      readme: '',
      isLoading: true
    }
  },

  computed: {
    siteName () {
      return this.$page.plugin.repo.split('/')[1]
    },
    githubUrl () {
      return `https://github.com/${this.$page.plugin.repo}`
    },
    netlifyDeployUrl () {
      return `https://app.netlify.com/start/deploy?repository=https://github.com/${this.$page.plugin.repo}`
    },
    codeSandboxUrl () {
      return `https://codesandbox.io/s/github/${this.$page.plugin.repo}`
    }
  },

  metaInfo () {
    return {
      title: this.$page.plugin.title
    }
  },

  async mounted () {
    const { repo } = this.$page.plugin
    const url = `https://api.github.com/repos/${repo}/readme`

    if (cache[repo]) {
      this.readme = cache[repo]
      this.isLoading = false
      return
    }

    this.isLoading = true

    const res = await fetch(url)
    const json = await res.json()
    const readmeRes = await fetch(json.download_url)
    const markdownSource = await readmeRes.text()

    this.readme = cache[repo] = markdown(markdownSource)
    this.isLoading = false
  },

  methods: {
    copyCommand () {
      clipboard(this.$refs.command.textContent)
    }
  }
}
</script>

<page-query>
query ($id: ID!) {
  plugin(id: $id) {
    title
    repo
    path
    preview
    screenshot(width: 1680, quality: 80)
    platforms {
      title
      logo(width: 25, height: 25)
    }
    author {
      title
      path
    }
  }
}
</page-query>

<style lang="scss">
.plugin {
  &__header {
    padding: 20px 10px 15px;
    font-size: .9rem;
    background-color: var(--bg-transparent);
    margin-top: -30px;
    margin-left: -10px;
    margin-right: -10px;
    z-index: 20;
    backdrop-filter: blur(4px);


    @media screen and (min-width: 850px) {
      position: sticky;
      top: calc(var(--header-height) + 20px);
    }
  }
  &__header-title {
    margin-right: .3rem;
  }
  &__header-author {
    color: currentColor;
    opacity: .5;
  }
  &__header-platform-logo {
    margin: 0 .5rem 0 0;
  }
  &__command-intro {
    margin-right: .5rem;
    opacity: .7;
  }
  &__command {
    span {
      flex: 1;
    }
  }
  &__image {
    img {
      border-radius: 5px;
      border: 1px solid var(--border-color);
      width: 100%;
    }
  }
}

.deploy-buttons {
  .button {
    margin-bottom: 0;
    margin-right: 1rem;
    svg {
      width: 20px;
      height: 20px;
      margin-right: .3rem;
    }
  }
}

.popover {
  &__container {
    position: absolute;
    top: 87%;
    right: -15px;
    z-index: 999;
    width: 500px;
    padding: var(--space);
    background-color: var(--bg);
    box-shadow: var(--glow);
    border-radius: 5px;
    border: 2px solid var(--border-color);
    animation: slideDown .3s;

    &:after, &:before {
      bottom: 100%;
      right: 57px;
      border: solid transparent;
      content: " ";
      height: 0;
      width: 0;
      position: absolute;
      pointer-events: none;
    }

    &:after {
      border-color: rgba(255, 255, 255, 0);
      border-bottom-color: var(--bg);
      border-width: 10px;
      margin-left: -10px;
    }
    &:before {
      border-color: rgba(204, 204, 204, 0);
      border-bottom-color: var(--border-color);
      border-width: 11px;
      margin-left: -11px;
    }
  }
}
</style>

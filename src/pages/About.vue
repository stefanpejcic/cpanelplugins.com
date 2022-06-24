<template>
  <Layout>
    <Section container="sm" class="text-center" style="max-width:1200px!important">
      <h1>About CpanelPlugins</h1>

      <p>CpanelPlugins is a github-hosted open-source collection of free cPanel plugins.</p>
	  <p>Hi there, I'm Stefan Pejcic - a Linux SysAdmin and WordPress plugin developer.
		I run a blog PCx3.com where I write mostly about Linux and cPanel. Recently when doing research for my new post: <a href="https://pcx3.com/cp/how-to-create-a-cpanel-plugin/">How to create a cPanel plugin</a> I discovered that publishing a cpanel plugin was pretty much the same as for a WordPress plugin, and woundered why 99% of plugins are premium. I decided to change that and publish a few cPanel plugins that I find useful such as Inode Usage Summary and Login Log.</br.
A few months later I was testing various Vue.js CMS's and encountered Gridsome. I did a few tutorials on <a href="https://pcx3.com/cp/how-to-install-gridsome-on-cpanel-shared-hosting/">How to install Gridsome on cPanel shared hosting</a> and while doing so, I fell in love with the simplicity and speed of Gridsome. Decided to use it instead my go-to CMS (WordPress) for a repository where one could download all my existing cpanel plugins.</p>
    </Section>
	<Section container="sm">
<p>To get your plugin listed, the following is required:</p>
<ul>
<li>Your plugin must be publicly available on Github.</li>
<li>installation script titled "install plugin.sh" must be included in the main branch.</li>
</ul>
</br>
<p>To add your plugin:</p>
<p>Fork this repo on Github: <a href="https://github.com/stefanpejcic/cpanelplugins.com" target="_blank">https://github.com/stefanpejcic/cpanelplugins.com</a></br>
Add your plugin information to the <a href="https://github.com/stefanpejcic/cpanelplugins.com/edit/master/plugins/plugins.yaml" target="_blank">plugins/plugins.yaml</a> file</br>
3. Make a pull request with the following title: ADD PLUGIN</p>
</br>
    </Section>
  </Layout>
</template>

<style lang="scss">
.logo-container {
	text-align: center;
	margin-bottom: var(--space);



	&--dark {
		background-color: var(--dark-bg);
	}

  &--secondary {
    background-color: var(--primary-color-dark);
  }

	a {
		display: block;
		padding: 10%;
	}
	img {
		max-width: 320px;
		width: 100%;
		margin: 0 auto;
	} 
}

.colors {
  text-align: center;
	div {
		padding: 15% 5% 5px;
		display: inline-block;
		margin: 0 .5rem;
		text-align: center;
		color:#FFF;
    outline: 1px solid rgba(0,0,0,.1);
	}


	&__primary {
		background-color: var(--primary-color);
	}

	&__secondary {
		background-color: var(--primary-color-dark);
	}

  &__dark {
    background-color: var(--dark-bg);
  }


}

</style>

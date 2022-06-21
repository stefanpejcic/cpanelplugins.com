<template>
  <Layout>
    <Section container="sm" class="text-center">
      <h1>About CpanelPlugins</h1>

      <p>CpanelPlugins is a github-hosted open-source collection of free cPanel plugins.</p>
    </Section>
	<Section container="sm" class="text-center">
<p>To get your plugin listed, the following is required:</p>
<p>- Your plugin must be publicly available on Github.</p>
<p>- An installation script titled "install plugin.sh" must be included in the main branch.</p>
</br>
<p>To add your plugin:</p>
<p>1. Fork this repo on Github</p>
<p>2. Add your plugin information to the XXX file</p>
<p>3. Make a pull request with the following title: ADD PLUGIN</p>
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

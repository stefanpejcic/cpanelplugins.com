<template>
  <nav class="main-nav flex gap-15">

    <g-link to="/starters/">
      <span class="main-nav__label">Plugins</span>
    </g-link>

    <g-link to="/scripts/">
      <span class="main-nav__label">Scripts</span>
    </g-link>

    <g-link to="/blog/">
      <span class="main-nav__label">Blog</span>
    </g-link>
	
	<g-link to="/about/">
      <span class="main-nav__label">About</span>
    </g-link>
  </nav>
</template>


<style lang="scss">
.main-nav {
  flex-wrap: nowrap;
}
@media screen and (max-width: 850px) {
 .main-nav {
    order: 10;
    min-width: 100%;
    a {
      padding-top: 5px;
      padding-bottom: 10px;
    }
  }
}
</style>

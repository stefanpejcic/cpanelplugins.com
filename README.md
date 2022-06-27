# cpanelplugins.com

<img src="https://raw.githubusercontent.com/stefanpejcic/cpanelplugins.com/master/plugins/screenshots/cpanel-plugins-homepage.png"></img>

CpanelPlugins is a github-hosted open-source collection of free cPanel plugins.

# How to add a plugin

To get your plugin listed, the following is required:

- Your plugin must be publicly available on Github.
- An installation script titled "installer.sh" must be included in the main branch.


To add your plugin:

1. Fork this repo[stefanpejcic/cpanelplugins.com](https://github.com/stefanpejcic/cpanelplugins.com)
2. Add your plugin information to the plugins/plugins.yaml file
3. Make a pull request with the following title: ADD PLUGIN


## How to add a blog post

1. Fork this repo[stefanpejcic/cpanelplugins.com](https://github.com/stefanpejcic/cpanelplugins.com)
2. Create a directory with the date and title of the post (e.g. 2022-06-26-cpanelplugins.com-is-live)
3. Create index.md file inside it with the actual blog post
4. Make a pull request with the following title: ADD POST


NOTE: The blog post (index.md) file must contain the following information at the top:

```
---
title | slug | author | date | excerpt
---
```

for example:

```
---
title: CpanelPlugins.com Is live 🎉🎉🎉
slug: cpanel-plugins-is-live
author: [stefanpejcic]
date: 2021-06-26
excerpt: "CpanelPlugins.com website is published!"
---
```
-------------

This is a fork of the gridsome.org website from 2022.

-------------

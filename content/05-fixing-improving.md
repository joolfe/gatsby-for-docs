---
title: "Improvements and adjustments"
metaTitle: "Improvements and adjustments"
metaDescription: "Steps for fix and improve the gatsby site"
---

# Fixing the navegation

The first thing that you will notice when test or recently deployed web (wow 🎉), is that navigation didn't work, if you click in any link on the left menu you will get this page:

![page 404 in git](../doc-img/404-in-git.png)

It's self explanatory, the links are not correct 😕, but why this happen? When we click in the second links for exmaple we get this in the browser `https://joolfe.github.io/02-setup-environment` and this page doesn't exist because the are a part missing in the path the repo name `gatsby-for-docs`, so the correct url should be `https://joolfe.github.io/gatsby-for-docs/02-setup-environment`.
After a ligth reading in the [documentation](https://www.gatsbyjs.org/docs/how-gatsby-works-with-github-pages/#github-repository-page) we found that need to set up an the property `pathPrefix` in config, to say gatbsy that we are not deployed in the root path of the domain.

So just go to the file `config.js` and update the property with value `gatsby-for-docs`, build again, publish and done 💪.

# Images

# Index page

# Urls 




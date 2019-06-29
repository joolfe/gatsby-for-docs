---
title: "Improvements and adjustments"
metaTitle: "Improvements and adjustments"
metaDescription: "Steps for fix and improve the gatsby site"
---

# Fixing the navegation

The first thing that you will notice when test or recently deployed web (wow 🎉), is that navigation didn't work, if you click in any link on the left menu you will get this page:

![page 404 in git](./doc-img/404-in-git.png)

It's self explanatory, the links are not correct 😕, but why this happen? When we click in the second links for exmaple we get this in the browser `https://joolfe.github.io/02-setup-environment` and this page doesn't exist because the are a part missing in the path the repo name `gatsby-for-docs`, so the correct url should be `https://joolfe.github.io/gatsby-for-docs/02-setup-environment`.
After a ligth reading in the [documentation](https://www.gatsbyjs.org/docs/how-gatsby-works-with-github-pages/#github-repository-page) we found that need to set up an the property `pathPrefix` in config, to say gatbsy that we are not deployed in the root path of the domain.

So just go to the file `config.js` and update the property with value `gatsby-for-docs`, build again, publish and done 💪.

# Images

Other problem that we can see at a glance is that images are not being loaded in our tutorial 😞

![image not load](./doc-img/no-image.png)

If we test in local in the develop server we can see that images are not loaded 😮, so should be the way that we are referencing images or where images are located.

Right now we have images in a folder called `/doc-img` in the root and we are referencing images from markdown using this code`![image not load](../doc-img/no-image.png)`.

# Complete the metainformation

Lot of info to be filled related with our page.

# Ups build files are collisioning!

Remove doc folder content before build.

# Urls 

The url of our page are not pretty.

# Index page

We are not filling this mdx page 






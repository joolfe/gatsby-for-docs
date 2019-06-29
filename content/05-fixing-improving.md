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

Right now we have images in a folder called `/doc-img` in root project level and we are referencing images from markdown using this code `![image not load](../doc-img/no-image.png)`.

I have found nothing related with images in the  [gatsby-gitbook-starter](https://www.gatsbyjs.org/starters/hasura/gatsby-gitbook-starter/) git repo or docs but to make builder understand that should take the images i think we should put inside the `/content` folder, here is where we are putting all our static content 😚. 

So we move our images to `/content/doc-img/` folder and in our markdown we are going to reference images as `![image not load](./doc-img/no-image.png)` (we just remove a point 😉). 

Now we should test in local so:

```
$ gatsby develop
```

and when we go to `http://http://localhost:8000` we can confirm that images are being loaded, awesome!!

Now just build, push and done 👌!

# Complete the metainformation

If we open `config.js` file we can see that there are lot of parameters that should be configured like
`title` or `githubUrl`, so this step is very easy just complete the info related with our site, as result we will have this:

```javascript
const config = {
	"gatsby": {
		"pathPrefix": "/gatsby-for-docs/",
		"siteUrl": "https://joolfe.github.io",
		"gaTrackingId": null
	},
	"header": {
		"logo": "https://graphql-engine-cdn.hasura.io/img/hasura_icon_white.svg",
		"title": "Gatsby gitbook tutorial",
		"githubUrl": "https://github.com/joolfe/gatsby-for-docs",
		"helpUrl": "",
		"tweetText": "",
		"links": [{ "text": "", "link": ""}],
	},
	"sidebar": {
		"forcedNavOrder": [],
		"links": [{ "text": "", "link": ""}]
	},
	"siteMetadata": {
		"title": "Gatsby gitbook tutorial",
		"description": "Step by step tutorial about how to use gatsby to create a gitbook doc.",
		"ogImage": null,
		"docsLocation": "https://github.com/joolfe/gatsby-for-docs/tree/master/content",
		"favicon": "https://graphql-engine-cdn.hasura.io/img/hasura_icon_black.svg"
	},
};

module.exports = config;
```

👉 We will change the logo url soon...

# Ups build files are collisioning!

Remove doc folder content before build.

# Urls 

The url of our page are not pretty.

# Right index 

Only first level is showed not sure if we should change for put second level also??

# Index page

We are not filling this mdx page 








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

# Build command is failling...

We have add a `mv` command in build script but after a couple of executions we get this error:

```
mv: rename public/static to docs/static: Directory not empty
```

An easy one... we are moving things without remove the previous files so we get this error 😢, to solve this we just need to add a `rm` command before move, so in the `package.json`script section we change for this:

``` json
  "scripts": {
    "build": "gatsby build --prefix-paths; rm -rf docs/*; mv public/* docs/"
  },
```

Thats all folks 🐷!

# Right nav bar erratic behaviour 

While testing in local I have seen that sometimes the right nav bar is not showed 😧 and testing in our pubished github pages confirm that there is a problem because is never showed 😱.

After do some test in local i have found a pattern, when the url finish with '/' the navbar is not showed, if we click in any link the last alsh desapear and then the navbar apper... is time to review the code. 

To see where the navbar is printed i just search for the literal `CONTENTS` (the title of the navbar) inside the `/src` folder and we get is in `src/components/rightSidebar.js` file (so foreseeable 😌).

If we see the code there is a `if else` for show or not the navbar:

```
if (finalNavItems && finalNavItems.length) {
        return (
          <Sidebar>
            <ul className={'rightSideBarUL'}>
              <div className={'rightSideTitle'}>CONTENTS</div>
              {finalNavItems}
            </ul>
          </Sidebar>
        );
      } else {
        return (
          <Sidebar>
            <ul>{finalNavItems}</ul>
          </Sidebar>
        );
      }
```

Basically depend of the definition of variable `finalNavItems` so looking for the definition code we foud just before the last lines and the critical point is this `if` statement:

```
if ((item.node.fields.slug === location.pathname) || (config.gatsby.pathPrefix + item.node.fields.slug) === location.pathname) {
```

Bascially is only setting a value to the variable if the actual `location.pathname` (is the page location) match one of the conditions, so to help us investigate i put this logs just before the `if` statement: 

```
console.log("Location: "+location.pathname);
console.log("Slug: "+item.node.fields.slug); 
console.log("Prefix + slug: "+config.gatsby.pathPrefix + item.node.fields.slug);
```

While testing in local using `$ gatsby develop` we see in the console this traces:

```
> Location: /02-setup-environment/
> Slug: 02-setup-environment 
> Prefix + slug: /gatsby-for-docs//02-setup-environment
```
😮 here we have the problem, in local when the url finish in `/` this is not cover by the conditions, but is easy to fix, we just add a new condition to the if like this:

```
(item.node.fields.slug+'/' === location.pathname)
```

One problem solved!, in the other side the problem in the published web is also obvious, if we see the last trace in the console there are an aditional slash in the url `/gatsby-for-docs//02-setup-environment` , this part of the path comes form `config.gatsby.pathPrefix` Ups 😗, thats something that we have setup in the `config.js` file, we have put:

```
	"gatsby": {
		"pathPrefix": "/gatsby-for-docs/",
		"siteUrl": "https://joolfe.github.io",
		"gaTrackingId": null
	},
```

so just replacing with this `/gatsby-for-docs` weare done 😎.

> Don't forget to remove the `console.log` code before publish again 😉.


# Google analytics 

One of the configuration value that we have left empty is the `"gaTrackingId"`, that is for Google Analitycs and track the visit in our tutorial webpage. 

To get this `id` you just need to be register in google, go to [analytics.google.com](https://analytics.google.com/analytics/web) and create a new account for track your web. Well is better descirbe [here](https://support.google.com/analytics/answer/1009694?hl=en) by Google 😬.

We put this value in our `config.js` file and done!







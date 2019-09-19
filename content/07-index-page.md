---
title: "Index page"
metaTitle: "Index page set up"
metaDescription: "We redirect from our root path to the introduction page directly."
---


# Index page

You probably have noticed, when you navigate to the tutorial page, the introduction page is not the correct one, like the picture below:

![Incorrect introduction](doc-img/incorrect-introduction.png)

In our `01-introduction.md` file we have different content, this is because when we access our tutorial page we are accessing to the `index.mdx` page, this page comes from the gatsby starter project, and I suppose is used like a landing page or something like that, you can see that  `index.mdx` page doesn't appear in the navbar.

We don't want a landing page because our web is just a tutorial, anyway we have two options:

1. Put additional information in this ´index.mdx´ file to show as startup page of our tutorial.
2. Try to redirect the load of the tutorial to the `01-introduction.md` page.

I prefer the second one because we don't have much more to say on our first page 😗.

# Redirecting root path

So what we need is when somebody put in the browser `https://joolfe.github.io/gatsby-for-docs/` show instead the URL `https://joolfe.github.io/gatsby-for-docs/01-introduction`.

After some minutes searching in google we get an example from the [gatsby Github repo](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-redirects/gatsby-node.js), and looks very easy, basically, we need to add the redirection rules in `gatsby-node.js` file, in our case inside the declaration `exports.createPages`  we will add this code:

```javascript
 const { createRedirect } = actions
 
 createRedirect({
 fromPath: `/`,
 isPermanent: true,
 redirectInBrowser: false,
 toPath: `/01-introduction`,
 })
```

To test we just execute `$ gatsby develop` and we can test in localhost that everything is working as expected, nice 💪!!

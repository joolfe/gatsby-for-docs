---
title: "Creating our new project"
metaTitle: "Creating our gatsby project"
metaDescription: "Steps about how to create a gatsby project using starters."
---

# Create a new gatsby project

The best way to create a new project in gatsby is using [starters](https://www.gatsbyjs.org/tutorial/part-zero/#create-a-gatsby-site), basically is a project template/skeleton from github with everything already set up to start coding, sounds great, isn't it?

Our idea is to create a tutorial and I love the [gitbook](https://www.gitbook.com/) style for this kind of static docs, so we are going to use as 'starter' this project [gatsby-gitbook-starter](https://www.gatsbyjs.org/starters/hasura/gatsby-gitbook-starter/) 

To create the new project again a terminal command is more than enough, you just need to select the new project folder name and the starter git URL using this command `gatsby new {folder_name} {starter_git_url}`. In our case let us use the command:

```bash
$ gatsby new gatsby-for-docs https://github.com/hasura/gatsby-gitbook-starter
```

In no time we will find a new folder created with a lot of things on it:

```bash
$ cd gatsby-for-docs/
$ ls
Dockerfile    README.md   content     gatsby-config.js  node_modules    package.json
LICENSE     config.js   doc.md      gatsby-node.js    package-lock.json src
```

Basically, this is a clone of the repo and a great start for us.

Before continuing let us check if our new project is working, gatsby comes with a develop server for test purpose, to build our new site and run in local we execute :

```bash
$ gatsby develop
```

After some seconds in our terminal we will see:

```bash
...
You can now view gatsby-gitbook-boilerplate in the browser.

 http://localhost:8000/

View GraphiQL, an in-browser IDE, to explore your site's data and schema

 http://localhost:8000/___graphql

Note that the development build is not optimized.
To create a production build, use npm run build

info ℹ ｢wdm｣: 
info ℹ ｢wdm｣: Compiled successfully.
```

Let us check in our browser the URL `http://localhost:8000/`, and that's what I have found, Great! 🚀

![First gatsby run](doc-img/first-run.png)


# Setup Git repo

We have our new project running and we don't want to lose our work... I know, I know... we have just executed a couple of commands 😗but we have created a new project and I don't want to lose anything, so let us set up our Github repo.

We already have an account on Github off course, so let us login into Github and create a new repo like shown in this image

![Create repo on github](doc-img/create-repo.png)

After clicking the **"Create Repository"** button we will see the next instructions in the screen that is shown

![New repo](./doc-img/new-repo.png)

So we go to the terminal and inside our project folder we are going to first add the remote origin with this command 

```bash
$ git remote add origin https://github.com/joolfe/gatsby-for-docs.git
```

And then we will do our first push

```bash
$ git push -u origin master
```

If we check again our repo we can see our files 😁.

> Maybe you prefer to use a tool like sourcetree for git, is a good idea 😉.
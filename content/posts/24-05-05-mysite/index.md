---
title: "Set Up My Blog Site with Github Pages + Hugo"
description: "How to create a website using Hugo and host iton GitHub"
date: 2024-05-05
tags: ["tools"]
author: "Me"
showToc: true
TocOpen: true
draft: false
hidemeta: false
comments: false
disableHLJS: true
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "1.jpg"
    caption: "yoru"
---

## 0. Prerequisites

- A [Github](https://github.com/) account

- [Hugo](https://gohugo.io/installation/)

## 1. Create your username.github.io repository

after creating the repository in github page, clone it to your local space with `ssh`

```bash
git clone git@github.com:username/username.github.io.git
```

replace `username` with your own github account username

## 2. Setup Hugo

Follow [Quick Start](https://gohugo.io/getting-started/quick-start/) guide to setup hugo and create a new site.

Make sure you install latest version of **`hugo(>=0.112.4)`**.

`cd` into your `username.github.io` folder

```bash
hugo new site mysite -f yml
```

then you will get a subfolder `mysite`

```bash
mv mysite/* .
rm -r mysite
rm hugo.toml
```

## 3. Install Hugo theme(PaperMod)

```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

for `UPDATE`: 

```bash
git submodule update --remote --merge
```

## 4. Config your site

add `config.yml` in `username.github.io` folder as follow:

```yml
baseURL: "http://username.github.io/"
title: ExampleSite
paginate: 5
theme: PaperMod

enableRobotsTXT: true
buildDrafts: false
buildFuture: false
buildExpired: false

minify:
  disableXML: true
  minifyOutput: true

params:
  env: production # to enable google analytics, opengraph, twitter-cards and schema.
  title: ExampleSite
  description: "ExampleSite description"
  keywords: [Blog, Portfolio, PaperMod]
  author: Me
  # author: ["Me", "You"] # multiple authors
  images: ["<link or path of image for opengraph, twitter-cards>"]
  DateFormat: "January 2, 2006"
  defaultTheme: auto # dark, light
  disableThemeToggle: false

  ShowReadingTime: true
  ShowShareButtons: true
  ShowPostNavLinks: true
  ShowBreadCrumbs: true
  ShowCodeCopyButtons: false
  ShowWordCount: true
  ShowRssButtonInSectionTermList: true
  UseHugoToc: true
  disableSpecial1stPost: false
  disableScrollToTop: false
  comments: false
  hidemeta: false
  hideSummary: false
  showtoc: true
  tocopen: true

  assets:
    # disableHLJS: true # to disable highlight.js
    # disableFingerprinting: true
    favicon: "<link / abs url>"
    favicon16x16: "<link / abs url>"
    favicon32x32: "<link / abs url>"
    apple_touch_icon: "<link / abs url>"
    safari_pinned_tab: "<link / abs url>"

  label:
    text: "Home"
    icon: /apple-touch-icon.png
    iconHeight: 35

  # profile-mode
  profileMode:
    enabled: false # needs to be explicitly set
    title: ExampleSite
    subtitle: "This is subtitle"
    imageUrl: "<img location>"
    imageWidth: 120
    imageHeight: 120
    imageTitle: my image
    buttons:
      - name: Posts
        url: posts
      - name: Tags
        url: tags

  # home-info mode
  homeInfoParams:
    Title: "Hi there \U0001F44B"
    Content: Welcome to my blog

  socialIcons:
    - name: x
      url: "https://x.com/"
    - name: stackoverflow
      url: "https://stackoverflow.com"
    - name: github
      url: "https://github.com/"

  analytics:
    google:
      SiteVerificationTag: "XYZabc"
    bing:
      SiteVerificationTag: "XYZabc"
    yandex:
      SiteVerificationTag: "XYZabc"

  cover:
    hidden: false # hide everywhere but not in structured data
    hiddenInList: false # hide on list pages and home
    hiddenInSingle: false # hide on single page

  editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link

  # for search
  # https://fusejs.io/api/options.html
  fuseOpts:
    isCaseSensitive: false
    shouldSort: true
    location: 0
    distance: 1000
    threshold: 0.4
    minMatchCharLength: 0
    limit: 10 # refer: https://www.fusejs.io/api/methods.html#search
    keys: ["title", "permalink", "summary", "content"]
menu:
  main:
    - identifier: categories
      name: categories
      url: /categories/
      weight: 10
    - identifier: tags
      name: tags
      url: /tags/
      weight: 20
    - identifier: example
      name: example.org
      url: https://example.org
      weight: 30
# Read: https://github.com/adityatelange/hugo-PaperMod/wiki/FAQs#using-hugos-syntax-highlighter-chroma
pygmentsUseClasses: true
markup:
  highlight:
    noClasses: false
    # anchorLineNos: true
    # codeFences: true
    # guessSyntax: true
    # lineNos: true
    # style: monokai
```

`config.yml` serves as a general configuration for all post

## 5. Create a post template

add `archetypes/post.md` as follow:

```yml
---
title: "Post Title"
description: "Post Description."
date: 2024-05-05
tags: ["TAG"]
author: "Me"
showToc: true
TocOpen: true
draft: false
hidemeta: false
comments: false
disableHLJS: true
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>"
    caption: "<text>"
---
```

then you can use it to create new blog by:

```bash
hugo new -k post posts/<blog-name>/index.md
```

## 6. Run Hugo locally

just type `hugo server`:

```bash
Start building sites …

                   | EN
-------------------+-----
  Pages            |  7
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  0
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Built in 32 ms

Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Open a browser and go to [**http://localhost:1313**](http://localhost:1313/)

you will see your blog running locally

## 7. Publish your blog to Github Pages

press `Ctrl+C` to stop

type `hugo`

```bash
rm -r docs
cp -r public docs
git add . && git commit -m "new hugo blog" && git push
```

Next, we need to **enable** GitHub Pages, which we can do by going to our GitHub repository and from there click on `Pages`. Enable it by changing the `Source` from `None` to `Deploy from a branch`

In `Branch` change `/(root)` to `/docs`, and `Save` your changes

After a short while, you will see that your blog is now published at [https://username.github.io](https://username.github.io/)

### End

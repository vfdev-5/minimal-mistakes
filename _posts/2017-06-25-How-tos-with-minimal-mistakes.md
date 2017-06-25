---
title: "How-tos with `minimal-mistakes`"
categories:
  - jekyll blog
tags:
  - jekyll
  - minimal-mistakes
  - html
---

How to make a `github.io` hosted site with `jekyll` and  [`minimal-mistakes` theme](https://github.com/mmistakes/minimal-mistakes).

First you need to fork the [minimal-mistakes repository](https://github.com/mmistakes/minimal-mistakes). Then you need to modify configuration files as it is described in [quick-start guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/).

### How to setup home page with a splash image

If you have `index.html` in the root folder, you can remove it. In `_config.yml` disable pagination:
```
# Outputting
permalink: /:categories/:title/
#paginate: 5 # amount of posts to show
#paginate_path: /page:num/
timezone: # http://en.wikipedia.org/wiki/List_of_tz_database_time_zones
```
Next, `_layouts/home.html` content looks like [here](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/home.md), namely
`layout: splash`.


### Header navigation tabs

This is controlled in `_data/navigation.yml`

### Write a post

Create a markdown file named `YYYY-MM-DD-Post-Short-Title.md` with a content:
```
---
title: "This title is shown if this field is specified, otherwise filename title is taken"
categories:
  - cat1
tags:
  - tag1
  - tag2
---
```

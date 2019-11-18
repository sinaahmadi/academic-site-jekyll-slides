---
title: Jekyll and GitHub Pages for Academics
description: Blogging made easy
theme: serif
---

## Outline

### Introduction
### Jekyll and GitHub Pages
### Creating your own website

----

## Introduction

### Why an academic webpage?

-   Control of your content
-   Reach people who are actively searching for you
-   A personal brand
-   A competitive advantage

~~

### Why Jekyll and GitHub Pages?
* Jekyll:
  - Transform your plain text into static websites and blogs.

* GitHib Page:
  - Free
  - Ad-free
  - Professional
  - All functionalities of version controlling

* **Jekyll has a built-in support for GitHub Pages**

~~

### Our objectives today
#### Practical session

* Learn to
  - Deploy your own academic website
  - Import your publications in *bibtex*
  - Add essential plugins
  - Create a blog
  - Add a commenting system

----

## Jekyll
### What is Jekyll?

- Ruby + Liquid + YAML = Jekyll!
- A blog-aware static site generator in Ruby
- Depends on templates, aka. layouts
- Ideal for personal, project, or organization sites
- The engine behind GitHub Pages
- Easily configurable

Read more about the [Jekyll philosophy](https://jekyllrb.com/philosophy/).

~~

### How does Jekyll work?

- Gathers content from `_post`, `_includes` and other files
- Applies a layout
- Converts Markdwon and Textile to HTML
- Runs Liquid converters
- Outputs static HTML pages in `_site` ready to be served by Apache, Nginx or other web servers.

~~

## Jekyll features

- Pagination
- Custom `permalink` structure
- Markdown/Textile conversion
- Syntax highlighting

~~

## Directory structure

A basic Jekyll site usually looks something like this:

```
.
├── _config.yml
├── _data
|   └── members.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid front matter
```

~~

### `_config.yml`

- YAML configuration
- Global configuration options 
- Per page/post configuration options (YAML front matter)
- Add your own key/value pairs and use them as you see fit

~~

### Setting up a Jekyll website

Once Jekyll is installed, you can create your new blog with the following command:

```
jekyll new YOUR_WEBSITE_NAME
```

Which will generates a folder with the following structure:

```
YOUR_WEBSITE_NAME/
  .gitignore
  _config.yml
  _includes
  _layouts
  _posts
  _sass
  about.md
  css
  feed.xml
  index.html
```

~~
## Deployment
Anywhere that can serve static pages including:
- Amazon S3
- GitHub Pages

----

## GitHub Pages

<iframe width="860" height="515" src="https://www.youtube.com/embed/2MsN8gpT6jY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

~~

> &ldquo; When Jekyll is used alongside GitHub, it will automatically re-generate all the HTML pages for your website each time you commit a file.&rdquo;

*Nota bene*: GitHub Pages does not support server-side languages such as PHP, Ruby, or Python.

~~

## Essential plugins

Github does not allow any but a few specific plugins to run for security reasons 🤷🏻‍♂️

- Local admin page: [jekyll-admin](https://github.com/jekyll/jekyll-admin)
- Generate site map: [jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap)
- Generate RSS feed: [jekyll-feed](https://github.com/jekyll/jekyll-feed)
- Importing bibliography: [jekyll-scholar](https://github.com/inukshuk/jekyll-scholar) ✖︎
- Generate post archives: [jekyll-archives](https://github.com/jekyll/jekyll-archives)
- Add metadata tags for search engines: [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag)

~~

### Themes

- Default themes: [https://pages.github.com/themes/](https://pages.github.com/themes/)
- [http://jekyllthemes.org/](http://jekyllthemes.org/)
- [https://jekyllthemes.io/](https://jekyllthemes.io/)

Learn how to create your own themes [here](https://jekyllrb.com/docs/themes/).


~~

### Types of sites

There are three types of GitHub Pages sites:
- user ➡ `<user>.github.io`
- organization ➡ `<organization>.github.io`
- project

You can only create **one** user or organization site for each GitHub account.

---- 

# Let's create a website

----

## Installation

### Instructions

* Install a full [Ruby development environment](https://jekyllrb.com/docs/installation/)
- [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/)
- [Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)
- [Jekyll on Windows](https://jekyllrb.com/docs/installation/windows/)
* Install Jekyll and bundler gems 

~~

### Gems

* Code you can include in Ruby projects
* package up functionality and share others
* Gems can perform functionality such as:
  - Converting a Ruby object to JSON
  - Pagination
  - Interacting with APIs such as GitHub

~~

### `Gemfile`

A `Gemfile` is a list of gems required for your site. 

```
source "https://rubygems.org"

gem "jekyll"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
end
```

~~ 

### Bundler 

Bundler installs the gems in your `Gemfile`

- `bundle install` to install the gems
- then `bundle exec jekyll serve` to build your site

If you’re not using a `Gemfile` you can just run `jekyll serve`

----

## `al-folio`

https://github.com/alshedivat/al-folio

----

## Commenting system

- [Disqus](https://disqus.com/)
- [Intense Debate](https://www.intensedebate.com/)
- Facebook comments

----  

## Typical workflow

- Add/update new content to your website
- Run locally using `jekyll serve`
- Push the changes to your `gh-pages` or `master` branch

----

## For more documentations
- [https://jekyllrb.com](https://jekyllrb.com)
- [GitHub Pages](https://pages.github.com/)
- More themes:
  * https://github.com/academicpages/academicpages.github.io
- [Jekyll tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)


---
## Thanks!

Any questions? 🙂


[Tutorial](tutorial.md) [Theme tutorial 1](theme-tutorial-01.md) [Theme tutorial 2](theme-tutorial-02.md)



# Adding an About page and a news section

# TODO: Lots of explanatory material.

Much of this is merely to try the code.

The next step is to add a news section. It could just as easily be a blog. 
You'll be able to add posts to the `/news` directory, and the home page
will automatically incorporate their titles into a News area on the
home page when you rebuild.

## What's in the Gutenberg directory structure

At the end of this section you'll have a site that looks like this:

```
┌── config.toml
├── public/
│   ├── index.html
│   ├── robots.txt
│   ├── sitemap.xml
│   ├── about/
│   │   └── index.html
│   └── news/
│       ├── page1/
│       │   └── index.html
│       ├── page2/
│       │   └── index.html
│       └── page3/
│           └── index.html
├── static/
├── themes/
│   ├── possibly other themes, such as hyde
│   └── step2-starter/
│       ├── theme.toml
│       ├── templates/
│       │   ├── index.html
│       │   ├── page.html
│       │   ├── section.html
│       │   └── simple.html
│       └── static/
├── content/
│   ├── _index.md
│   ├── about.md
│   └── news/
│       ├── _index.md
│       ├── page1.md
│       ├── page2.md
│       └── page3.md
├── sass/
└── templates/

```

## Build the directory structure

### Create a subdirectory under `/themes/step2-starter` using your new theme name

* Create a new directory for your new theme in the `/themes` directory and move into it.

```
# Wherever you see starter, replace it with the
# name of your own theme.
# The -p option lets you create subdirectories nested to
# any depth.
$ mkdir -p ~/www/themes/step2-starter

# Make it the current direcdtory
$ cd ~/www/themes/step2-starter

# Create this theme's (so far unused) `/static` directory
$ mkdir static

# Create this theme's `/templates` directory
$ mkdir templates

```

## Create the file /themename/theme.toml

Copy the previous `theme.toml`, changing only its `name`, and place in the `step2-starter` theme directory:

```
# Name of the theme itself
name = "step2-starter"

# Executive summary for directories of themes
description = "A minimal Gutenberg theme with a typical feature set"

# MIT is the obvious license because Gutenberg uses it
license = "MIT"

# Where to find this theme's source
homepage = "https://github.com/tomcam/gutenberg-starter"

# Minimum version of Gutenberg required for this theme
min_version = "0.2.2"

[author]

# Creater of original theme
name = "Tom Campbell"

# Homepage of the theme creator (not the theme itself)
homepage = "https://tom.im"

```

## Create the template files

Template files add HTML formatting to the textual contenet in the Markdown (`.md`) files found in the `/content` directory.

### Create the index template file `/themename/templates/index.html`


```html

<!DOCTYPE html>
<html lang="en-us">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="{{ config.description }}">
    <title>{{ config.title }}</title>
    <link rel="stylesheet" 
href="https://cdnjs.cloudflare.com/ajax/libs/spectre.css/0.2.10/spectre.min.css" />
</head>
<body>
    <div class="container">
        <div class="columns">
            <div class="col-9">


[//]: # ({% raw %})
    
                {% block content %}
                    {{ section.content | safe }}
                {% endblock content %}

[//]: # ({% endraw %}) 

            </div><!-- .col-9 -->
            <div class="col-3">
                <h1>News</h1>
                {% set section = get_section(path="news/_index.md") %}
                {% for page in section.pages %}
                    <h4>{{ page.date }}</h4>
                    <h3>
                        <a href="{{ page.permalink }}">
                        {{ page.title | safe }}</a>
                    </h3>
                {% endfor %}
            </div><!-- col-3 -->
        </div><!-- columns -->
    </div><!-- .container -->
</body>
</html>


```

### Create the page template file `/themename/templates/simple.html`

```html
{% extends "index.html" %}
{% block content %}
    {{ page.content | safe }}
{% endblock content %}
```
                                 
### Create the page template file `/themename/templates/page.html`

```html
<!DOCTYPE html>
<html lang="en-us">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="{{ config.description }}">
    <title>{{ page.title }}</title>
    <link rel="stylesheet"  href="https://cdnjs.cloudflare.com/ajax/libs/spectre.css/0.2.10/spectre.min.css" />
</head>
<body>
    <h4>{{ page.date | date(format="%Y-%m-%d") }}</h4>
    {{ page.content | safe }}
    <p>Word count: {{ page.word_count }}</p>
    <p><a href="{{ page.permalink }}">Permalink</a>
    <a href="{{ get_url(path="./_index.md") }}">Home</a></p>
</body>
</html>
```

### Create the section template file `/themename/templates/section.html`

```html
<!DOCTYPE html>
<html lang="en-us">
<title>Starter theme</title>
```

## Create the text content of the site

This tutorial shows you how to create a `/news` section for your site. Gutenberg will, at the direction of this theme, place all the files in the `/content/news` directory on the home page in their own `News` column to the right of the main content. This placement is arbitrary HTML and they could just as easily be to the left or below the main content area.

The articles have different dates. The template sorts them from newest to oldest order.

The titles of the articles are also arbitrary, but they will become part of the URL. There's no reason to name them 
`page1.md`, `page2.md`, etc. They couild just as well be named `theme-tutorial-debuts.md`, `second-part-announced.md`, and so on.

Here we'll create the `/news` section and three sample articles.

### TODO: Finish explanation

## Create the `content/about.md` page

We're going to create another static page on the site. It's considered good form (and good search engine mojo) to have a number of standard pages on your site such as About, Contact, Terms of Service, and so on. These pages would formatted minimally using the `simple.html` template. We'll have one such example page, About.

```
+++
title = "About"
template = "simple.html"
+++

# About this site

This a fine site

Go [home](/)
```

### Create the article `content/news/_index.md`

```
+++
title = "News section"
sort_by = "date"
+++
```

### Create the article `/content/news/page1.md`

```
+++
title="Theme tutorial debuts"
template="page.html"
date="2017-12-01"
+++

# How to create a theme in Gutenberg 

Gutenberg themes are based roughly on those of Hugo,
a competing static blogging platform.
```

### Create the article `content/news/page2.md`

```
+++
title="Second part of theme tutorial announced"
template="page.html"
date="2017-12-02"
+++

# Gutenberg themes: adding a section 

The earlier tutorial was the simplest possible: a single
page. This builds on that concept by adding a directory
full of articles.

```

### Create the article `content/news/page3.md`

```
+++
title="Derived from title?"                                      
template="page.html"
date="2017-12-03"  
+++ 

# Page 3 announced 

Who doesn't love page 3?

```


[Tutorial](tutorial.md) [Theme tutorial 1](theme-tutorial-01.md) [Theme tutorial 2](theme-tutorial-02.md)

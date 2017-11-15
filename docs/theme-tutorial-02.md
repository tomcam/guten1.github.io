# Adding a news section

# TODO: Lots of explanatory material.

Much of this is merely to try the code.

The next step is to add a news section. It could just as easily be a blog. 
You'll be able to add posts to the `/news` directory, and the home page
will automatically incorporate their titles into a News area on the
home page when you rebuild.

### Create a subdirectory under `/themes/step2-starter` for the new theme name

* Create a new directory for your new theme in the `/themes` directory and move into it.

```
# Wherever you see starter, replace it with the
# name of your own theme.
# The -p option lets you create subdirectories nested to
# any depth.
$ mkdir -p ~/www/themes/step2-starter/templates

# Make it the current direcdtory
$ cd ~/www/themes/step2-starter/templates

```

Create the template file index.html:

```html
<!DOCTYPE html>
<html lang="en-us">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<meta name="description" content="{{ config.description }}">
	<title>{{ config.title }}</title>
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/spectre.css/0.2.10/spectre.min.css" />
</head>
<body>
	{{ section.content | safe }}
	<h1>News</h1>
	{% set section = get_section(path="news/_index.md") %}
	{% for page in section.pages %}
		<h4>{{ page.date }}</h4>
		<h3><a href="{{ page.permalink }}">{{ page.title | safe }}</a><h3>
	{% endfor %}
</body>
</html>
```

Create the template file page.html:

```html
<!DOCTYPE html>
<html lang="en-us">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<meta name="description" content="{{ config.description }}">
	<title>{{ page.title }}</title>
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/spectre.css/0.2.10/spectre.min.css" />
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

Create the template file section.html:

```html
<!DOCTYPE html>
<html lang="en-us">
<title>Starter theme</title>
```

Create the article content/news/page1.md

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

Create a second article, named content/news/page2.md

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

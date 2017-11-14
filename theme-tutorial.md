# How to write a Gutenberg theme

## 

* Go to your Gutenberg home directory. Here the home directory is in `~/www/` but there is no reason, convention or otherwise, 
that you need to use the same directory.

```bash
# Make the Gutenberg directory the current one.
$ cd ~/www
```

### Create a subdirectory under `/themes` using your new theme name

* Create a directory for your customer them in the `/themes` directory and move into it.

```
# Whereever you see starter, replace it with the
# name of your own theme.
$ mkdir themes/starter

# Make it the current direcdtory
$ cd themes/starter

```

### Create a TOML file named theme.toml

* Create an empty TOML file for this theme named `theme.toml`.

```
# Create a new file. This could be done just as easily
# with an editor, for example, vim themes/starter/theme.toml
$ touch theme.toml
```

* Populate your `theme.toml` file with configuration info. Note that lines starting with `#` are comments.

```
# Name of the theme itself
name = "starter"

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

### Create a `/themename/static` directory

Even if it's not used, your theme is expected to have a /static directory.

* Create a directory named `/themename/static`:

```bash
$ mkdir static
```

### Create an index.html template in the /themename/templates directory

All themes require a file in the `/themename/templates` subdirectory named `index.html`. (Obviously
replace `/themename` with whatever you've named your theme.)

* Create a directory named `/templates` under the directory you've created for your theme.

```bash
$ mkdir templates
```

* Underneath it create the file `index.html`

```bash
$ vim index.html
```

* Populate the `index.html` template as follows and save it:

```html
<!DOCTYPE html>
<html lang="en-gb">
    <head>
        <meta charset="UTF-8">
        <meta name="apple-mobile-web-app-capable" content="yes">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <meta name="description" content="{% block description %}{{ config.description }}{% endblock description %}">
        <title>{% block title %}{{ config.title }}{% endblock title %}</title>
		<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/spectre.css/0.2.10/spectre.min.css" />
    </head>
    <body>
    	{% block content %}
    		{{ section.content | safe }}
    	{% endblock content %}
    </body>
</html>
```

### Create the article file `_index.md`

* Create the following text file and name it `_index.md`:


```
+++
title = "The Starter theme for Gutenberg"
template = "index.html"
date = "2017-12-11"
+++

# A simple Gutenberg theme called Starter

[Starter](https://github.com/tomcam/gutenberg-starter) is 
a fairly minimalist theme for the Gutenberg 
static site generator.
```

### Regenerate the site with `gutenberg build`

Since fundamental files have changed, you need to regenerate the site. 

```bash
$ gutenberg build
```

Now take a look at the results in your browser:

![Stripped down index.html home page](images/gutenberg-starter-theme-step1.png)


## The theme explained

You have probably guessed that constructs such as '{{ config.title }}` represent values that get replaced
when the published HTML is generated from an HTML template and the Markdown source file.

`{{ config.title }}` gets replaced with the specified by the `title` line in `config.toml`:

### file `themename/config.toml`:

```
# Appears on browser tabs & often in search results 
title = "Simple starter template"
```


# Todo

* Do a lesson on an anonymous theme
* Find out the correct term for what I call an anonymous theme
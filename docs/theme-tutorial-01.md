# How to write a Gutenberg theme

This first step shows you how to write a complete Gutenberg theme for a site that
has only one page: the home page.

## What's in the Gutenberg directory structure

### TODO: Full directory structure probably belongs in another section

At the end of this section you'll have a site that looks like this:

```
┌── config.toml
├── public/
│   ├── index.html
│   ├── robots.txt
│   └── sitemap.xml
├── static/
├── themes/
│   └── starter/
│       ├── theme.toml
│       ├── templates/
│       │   └── index.html
│       └── static/
├── content/
│   └── _index.md
├── sass/
└── templates/

```

`public` directory
: The `public` directory is generated automatically

`themes` directory
: The `themes` directory can contain multiple themes. `config.toml` controls which theme is currently in use

## Building the theme

The theme built in this tutorial looks like this:

```
themes/
└── starter/
    ├── theme.toml
    ├── templates/
    │   └── index.html
    └── static/
```

The `static` directory must be included although it's not used in this example.

* Go to your Gutenberg home directory. Here the home directory is in `~/www/` but there is no reason, convention or otherwise, 
that you need to use the same directory.

```bash
# Make the Gutenberg directory the current one.
$ cd ~/www
```

### Create a subdirectory under `/themes` using your new theme name

* Create a directory for your custom theme in the `/themes` directory and move into it.

```
# Whereever you see starter, replace it with the
# name of your own theme.
$ mkdir themes/starter

# Make it the current direcdtory
$ cd themes/starter

```

### Create the file /themename/theme.toml

* Create an empty TOML file for this theme named `theme.toml`
and add these contents. Note that lines starting with `#` are comments.

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

Even if though it's not used in this example, your theme is expected to have a /static directory.

* Create a directory named `/themename/static`:

```bash
$ mkdir static
```

### Create /themename/templates/index.html file

All themes require a file in the `/themename/templates` subdirectory named `index.html`. (Obviously
replace `/themename` with whatever you've named your theme.)

* Create a directory named `/templates` under the directory you've created for your theme.

```bash
$ mkdir templates
```

* Change to that directory and create the file `index.html` as shown:

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
 </body>
</html>

```

### Create the file `/content/_index.md`

* Return to the root of your project directory:

```bash
$ cd ../content
```

* Create the following text file and name it `_index.md` and give it these contents:

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

## Update `config.toml` with the name of the new theme

The theme is done. Now let Gutenberg know it should be put to use.

* Return to the main Gutenberg directory (not a theme directory):

```bash
# Change this to the base Gutenberg page for your
# installation.
$ cd .. 
```

* Fire up you favorite editor, load `config.toml`, and put this anywhere above the `[extra]` line:

```
# Replace with the name of your theme
theme = "starter"
```

### Regenerate the site with `gutenberg build`

Since fundamental files have changed, you need to regenerate the site. 

```bash
$ gutenberg build
```

### Run the server if necessary

If the Gutenberg server isn't running, fire it up:

```bash
$ gutenberg serve
```

Now take a look at the results in your browser by visiting `https://127.0.0.1:1111`

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

* Finish "The theme explained"
* Do a lesson on an anonymous theme
* Find out the correct term for what I call an anonymous theme

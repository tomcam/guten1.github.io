[Tutorial](tutorial.md) [Theme tutorial 1](theme-tutorial-01.md) [Theme tutorial 2](theme-tutorial-02.md)


# How to write a Gutenberg theme

This first step shows you how to write the simplest possible Gutenberg theme: it is for a site with only one page. If that seems too reductive, keep in mind that many new sites start out with a simple home page designed to get people interested in coming events or products.

## What's in the Gutenberg directory structure

At the end of this section you'll have a site that looks like this:

```
┌── config.toml
├── public/
│   ├── index.html
│   ├── robots.txt
│   └── sitemap.xml
├── static/
├── themes/
│   └── step1-step1-starter/
│       ├── theme.toml
│       ├── templates/
│       │   └── index.html
│       └── static/
├── content/
│   └── _index.md
├── sass/
└── templates/

```

### `/config.toml` file

Overall configuration for your Gutenberg-generated website, including the active theme

### `/public` directory

Most HTML files in the `public` directory are generated automatically by combining articles 
written in Markdown format in the `/content` directory and HTML files in the theme's `templates`
directory

### `/static` directory

Contains assets such as graphics files, fonts, or style sheets used by the site as a whole. Unused in this example.

### `/themes` directory

The `themes` directory can contain multiple themes. `config.toml` controls which theme is currently in use. Each directory immediately underneath is the name of a theme, and is the name used by `config.toml` to load the active theme. The only theme in this example is named `step1-starter`.

### `/themes/step1-starter/theme.toml` file

Each theme requires a `theme.toml` file with information about that theme, all of which is accessible at runtime and assists consumers of the theme. For example, the `homepage` item tells where the home page originated, and can be used in theme directories.

### `/themes/step1-starter/templates` directory

The theme's `/templates` directory contains HTML files that include special values known to Gutenberg. They provide formatting when the Markdown `.md` source files are converted into plain HTML for rendering. While this
example is the smallest possible theme and provides only a single home page (`index.html`), it's common to have at least one more template type called `page.html` to format blog posts or news articles. You can use as many different kinds of template files as you wish. (Replace `step1-starter` in the example above with the name of a particular theme, like `hugo` or `starter`.)

### `/themes/step1-starter/static` directory

Contains assets such as graphics files, fonts, or style sheets used solely by this theme. Unused in this example.  (Replace `step1-starter` in the example above with the name of a particular theme, like `hugo` or `starter`.)

### `/content` directory

Contains the Markdown `.md` source files with the actual text content of the site. They are converted into plain HTML for rendering in combination with associated template files files from the `/themes/step1-starter/templates` directory. Each Markdown or `.md` file has front matter specifying which HTML template would be used for this file. In this example, `_index.md` has the line `template = "index.html"` in its front matter. ( (Replace `step1-starter` in the example above with the name of a particular theme, like `hugo` or `starter`.)

In a production site with more than one page the content would have many, many more files, with names like `12-17-2018.md`, and they would probably be arranged into subdirectories. This would result in URLS like `example.com/blog/12-17-2018.md` or `example.com/staff/jared/profile.md`

### `/sass` directory

For [Sass](http://sass-lang.com/) CSS source files. For the case where the site has an unnamed anonymous theme. Unused in this example.

### `/templates` directory

Same as the `/themes/step1-starter/static` directory. For the case where the site has an unnamed anonymous theme. Unused in this example.


## Building the theme

The theme built in this tutorial looks like this:

```
themes/
└── step1-starter/
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
$ mkdir themes/ (Replace `step1-starter` in the example above with the name of a particular theme, like `hugo` or `starter`.)

# Make it the current direcdtory
$ cd themes/step1-starter

```

### Create the file /step1-starter/theme.toml

* Create an empty TOML file for this theme named `theme.toml`
and add these contents. Note that lines starting with `#` are comments.

```
# Name of the theme itself
name = "step1-starter"

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

### Create a `/step1-starter/static` directory

Even if though it's not used in this example, your theme is expected to have a /static directory.

* Create a directory named `/step1-starter/static`:

```bash
$ mkdir static
```

### Create /step1-starter/templates/index.html file

All themes require a file in the `/step1-starter/templates` subdirectory named `index.html`. (Obviously
replace `/step1-starter` with whatever you've named your theme.)

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

### file `step1-starter/config.toml`:

```
# Appears on browser tabs & often in search results 
title = "Simple starter template"
```

# Todo

* Finish "The theme explained"
* Do a lesson on an anonymous theme
* Find out the correct term for what I call an anonymous theme

[Tutorial](tutorial.md) [Theme tutorial 1](theme-tutorial-01.md) [Theme tutorial 2](theme-tutorial-02.md)


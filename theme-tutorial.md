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
name = "starter"
description = "A minimal Gutenberg theme with a typical feature set"
license = "MIT"
homepage = "https://github.com/tomcam/gutenberg-starter"
min_version = "0.2"

[extra]

[author]
name = "Tom Campbell"
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


# Todo

* Do a lesson on an anonymous theme
* Find out the correct term for what I call an anonymous theme

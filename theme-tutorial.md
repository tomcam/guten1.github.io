# How to write a Gutenberg theme

## 

* Go to your Gutenberg home directory. Here the home directory is in `~/www/` but there is no reason, convention or otherwise, 
that you need to use the same directory.

```bash
# Make the Gutenberg directory the current one.
$ cd ~/www
```

### Create a subdirectory under `/themes` using your new theme name

* Create a directory for your customer them in the `/themes` directory.

```
# Whereever you see starter, replace it with the
# name of your own theme.
$ mkdir themes/starter

```

### Create a TOML file named theme.toml

* Create an empty TOML file for this theme named `theme.toml`.

```
# Create a new file. This could be done just as easily
# with an editor, for example, vim themes/starter/theme.toml
$ touch themes/starter/theme.toml
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


# Todo

* Do a lesson on an anonymous theme
* Find out the correct term for what I call an anonymous theme

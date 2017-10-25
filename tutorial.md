# Gutenberg Tutorial: Using the Gutenberg static website generator

[Gutenberg](https://getgutenberg.io) lets you create high-performance websites quickly. 
It converts text files using a simple formatting language known as Markdown or [CommonMark](http://commonmark.org/) 
into HTML files via the command line. The finished site is pure HTML and therefore it is likely to be much faster
than similar websites created using WordPress.

This tutorial shows you how to:

1. Use Gutenberg from the command line to generate a minimal site on your local machine
2. Obtain a theme from the Web so you don't have to create a style sheet from scratch
3. Run Gutenberg as a local web server so you can see the site as users well

You will iterate through steps 2 and 3 many times in the course of the tutorial. When you edit the Markdown file used
for your website's content pages, Gutenberg detects the changes, compiles the HTML files from Markdown files, and deploys them
to the site's HTML directly continuously. This combines the best feature of an interactive site editor (quick
and responsive) with the joys of working with text (less distracting, can be done with light system resource
usage, and doesn't lock you in to any vendor's software).

## When to use Gutenberg and when not to

Gutenberg specializes in the creation of static sites. It is not really meant to be used for data-driven sites.

### When to use Gutenberg

Gutenberg excels at creating small to medium sites with some or all of these characteristics

* Brochure sites
* Academic styles
* Blogs
* News sites, divided into sections
* Personal sites

### When to avoid Gutenberg

Gutenberg doesn't work like WordPress, which stores its articles in a database, then renders and formats them
each time they are viewed. This data-driven approach means that interactive featuers like
discussion threads

## Pros and cons of using Gutenberg to generate your static website

Here are reasons both for and against using Gutenberg.

### Gutenberg Pros

* The websites Gutenberg creates are normally small and very fast
* Because the text files you use to create articles and posts using Gutenberg is based on Markdown, it's 
very easy to read them. None of the angle bracket madness you'll see in HTML.
This lets you concentrate on writing articles instead of counting angle brackets or HTML tags and attributes.
* Once you know how to use the toolchain, Gutenberg lets you generate sites quickly
* You can automate the creation and maintenance of websites
* You only need a single executable file
* Has [Sass](http://sass-lang.com/guide) built in (no external programs are run) so
maintaining style sheets is easier, especially on big projects
* It's free, even for commercial use, and [the source code to Gutenberg is available on Github](https://github.com/Keats/gutenberg)
* Excellent community. Gutenberg's creator, [Vincent Prouillet](https://github.com/Keats), is responsive and tolerates
dumb questions with patience

### Gutenberg Cons

* It's a command-line utility. You pretty much have to be a programmer/devops person to 
use Gutenberg. Installing it, which means downloading a single file and copying it to a directory,
is marginally harder then just clicking an installer.

## What you should know before running this tutorial

This tutorial assumes you know:

* HTML and CSS basics
* How to use a plain text editor
* How to start and stop the terminal program for your operating system 
* How to perform simple command-line operations such as copying and deleting files

## What you don't need to know before running this tutorial

You don't need to know about using competing products such as WordPress, Jekyll, or Hugo. From time to time they'll come up as points of reference but nothing require their prior use. You don't need to be an HTML or CSS expert.
 
## How this tutorial works

This tutorial takes you almost keystroke-by-keystroke through everything you need to create a functioning
corporate website with a home page, an About page, different sections, and a blog. You will be shown how to:

* Download Gutenberg and copy it to a directory on the path
* Use it to generate a stub website
* Copy a theme to make styling your website easier
* Edit the text files necessary to create the site

## Download Gutenberg

The first thing to do is obtain the Gutenberg static site generator. It is small and fast, and because it's a command-line utility written in Rust, Gutenberg works on all operating systems that have a Rust compiler and a web server available to them. You don't need to know Rust to use Gutenberg effectively, although understanding Rust's templating will make it easier
for you to create Gutenberg themes.

At the time of writing, Gutenberg lacks installers for most operating systems but that barely matters. It consists of a single executable file you run from the command line.

* Follow the download instructions at www.getgutenberg.io
* Copy the executable to a location on the path. For example, on Macs and many Linux variations the following would work:

```sh
# Copy from the OS X Downloads directory to a location on the path.
# In many operating systems, ~ means the user's home directory,
# sort of like My Documents on Windows.
# sudo means run from an elevated adminstrator level.
# It is not always necessary and depends on the operating system.
$ sudo cp ~/Downloads/gutenberg /usr/local/bin/
```

The site will be deployed from a directory of your choice. For various reasons
I like it to come from a subdirectory on my machine using a convention similar
to some web hosts, which often treat a site name something like `www` as the
first place on the path they look to server web pages from.

```sh 
# Create a site source code directory
# It can be named anything, but often web
# servers deploy from a directory with a name 
# similar to this one.
# This only needs to be done once.
# So the site source code will end up in 
# directories named like this:
# ~/www/mycharity ~/www/myhomepage ~/www/mysoccerteam
$ mkdir ~/www 
```

* Now change to the directory you just created:

```sh
#  Go where all your site source code will be.
$ cd ~/www
```

* From this starting directory you'll run Gutenberg, which will
generate a simple site:

```sh
# Replace mywebsite with the root name of your site, like bobsrestaurant or whatever.
$ gutenberg init mywebsite
```

* You are asked a short series of questions.

```
Welcome to Gutenberg!

> What is the URL of your site? (https://example.com): http://127.0.0.1:1111
> Do you want to enable Sass compilation? [Y/n]: y 
> Do you want to enable syntax highlighting? [y/N]: y

Done! Your site was created in "/Users/tom/www/mywebsite"
```

* Take a look at the contents of the directory that it just created. You've
created something! Let's see what it looks like.

## XXX Todo: explain these directories

```sh
$ ls mywebsite
config.toml	sass		templates
content		static		themes
```

## Install a Gutenberg theme

Before you see what the site looks like, install a theme. It
will be easier to see what kind progress you're making as you build
your new site.

* Go to the themes directory for your site:

```sh
$ cd ~/www/mywebsite/themes
```

* Obtain the Hyde theme from Github.

```sh
$ git clone https://github.com/Keats/hyde.git
```

This creates a directory named `hyde` (at `~/www/mywebsite/themes/hyde`) populated by other directories and files that make up that theme. 

After a pause you see the following:

```
Cloning into 'hyde'...
remote: Counting objects: 32, done.
remote: Total 32 (delta 0), reused 0 (delta 0), pack-reused 32
Unpacking objects: 100% (32/32), done.
```

* Now take a look:

```sh
$ ls
hyde
```

## Update config.toml with name of current theme

Now you need to specify to Gutenberg what theme is being used (because you could put other
themes in the `/themes` directory).

* Return to the site's root directory:

```sh
cd ~/www/mywebsite
```

* Open the file `config.toml` in a text editor.

8 Add this line to config.toml anywhere ABOVE the section marked `[extra]`:

```
theme = "hyde"
```

So it looks something like this:

```
theme = "hyde"

[extra]
# Put all your custom variables here
```

## Build the site

Now it's time to convert the site's stub .md files to HTML. Gutenberg combines HTML templates
with the markup files, and the output is pure HTML files the browser can understand.

```sh
$ gutenberg build
Building site...
-> Creating 0 pages (0 orphan) and 0 sections
Done in 22ms.
```

## View the site

Gutenberg can run as a web server, allowing you to view the site exactly as end users will see it upon publishing
to the production server.

You should open a new terminal window for this because the server runs in a loop waiting for web requests.
You'll want another terminal open so you can view files and directory contents.

* Open a new terminal window.
* Change to the project directory. In this case, you'd do something like this:

```sh
cd ~/www/mywebsite
```
* Run the server;

```sh
$ gutenberg serve
Listening for changes in /Users/tom/www/mywebsite/{content, static, templates, sass}
Web server is available at http://127.0.0.1:1111
```

* To view your handywork, open a browser and copy in the address `http://127.0.0.1:1111`:

An empty site appears.


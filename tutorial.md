# Gutenberg Tutorial: Using the Gutenberg static website generator

[Gutenberg](https://getgutenberg.io) lets you create high-performance websites quickly. 
It converts text files using a simple formatting language known as Markdown or [CommonMark](http://commonmark.org/) 
into HTML files via the command line. The finished site is pure HTML and therefore it is likely to be much faster
than similar websites created using WordPress.

## When to use Gutenberg and when not to

Gutenberg specializes in the creation of static sites. It is not really meant to be used for data-driven sites.

### When to use Gutenberg

### When to avoid Gutenberg

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

This tutorial assumes you know

* HTML and CSS basics
* How to start and stop the terminal program for your operating system

## What you don't need to know before running this tutorial

You don't need to know about using competing products such as WordPress, Jekyll, or Hugo.
 
## How this tutorial works

This tutorial takes you almost keystroke-by-keystroke through everything you need to create a functioning
corporate website with a home page, an About page, different sections, and a blog.



About to create a local-only test site named example, as if it were on example.com
Downloaded gutenberg at www.getgutenberg.io
Copied it to the path:
$ sudo cp ~/Downloads/gutenberg /usr/local/bin/
Created a directory for the website:
$ cd ~
$ mkdir  www  # Could be named anything. www is not required.
Create a stub project
$ cd www
$ gutenberg init blogcertification

Welcome to Gutenberg!
> What is the URL of your site? (https://example.com): http://blogcertification.com OR http://127.0.0.1:1111
> Do you want to enable Sass compilation? [Y/n]: y or press Enter to accept Y, the default as you can tell because it's uppercase
> Do you want to enable syntax highlighting? [y/N]: y

Done! Your site was created in "/Users/tom/www/blogcertification"

Take a look at the contents of the directory
$ ls blogcertification
config.toml	sass		templates
content		static		themes

Installing a Gutenberg theme
Go to the themes directory for your site.
$ cd blogcertification/themes
Obtain a theme from Github.
$ git clone https://github.com/Keats/hyde.git
This will create a directory named hyde populated by other directories and files that make up that theme. 
After a pause you see the following:

Cloning into 'hyde'...
remote: Counting objects: 32, done.
remote: Total 32 (delta 0), reused 0 (delta 0), pack-reused 32
Unpacking objects: 100% (32/32), done.
Now take a look:
$ ls
hyde
Now you need to specify what theme is being used, and the URL of the site.
Return to the site's root directory;
cd ..
Bring up config.toml in your editor. For example:
$ vim config.toml
Add this line to config.toml ABOVE the section marked [extra]:

theme = "hyde"

So it looks something like this:

theme = "hyde"
[extra]
# Put all your custom variables here

Generate the site:

$ gutenberg build
Building site...
-> Creating 0 pages (0 orphan) and 0 sections
Done in 22ms.


Viewing the site
Get started by using the built-in server: `gutenberg serve`
* Run the server

$ gutenberg serve
Listening for changes in /Users/tom/www/blogcertification/{content, static, templates, sass}
Web server is available at http://127.0.0.1:1111
Open a browser and copy in the address http://127.0.0.1:1111
An empty site appears.


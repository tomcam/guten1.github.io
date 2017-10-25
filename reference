# Reference

[GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/)

## Error messages


### Filter `date` received an incorrect type 

Appears as part of this error message:

```
Failed to build the site
Error: Failed to render section ''
Reason: Failed to render 'hyde/templates/index.html'
Reason: Filter `date` received an incorrect type for arg `value`: got `Null` but expected i64|u64|String
```

Cause: a markdown page expected a date in the front matter but didn't have one.

Example: Imagine a file named `main.md` in the `/content` directory with the following contents:

```
title = "title here" 
template = "page.html"
+++

hello, world.
```

The **Filter `date` received an incorrect type** error message appears until the `main.md` illustrated above gets
a properly formatted date in the front matter, like this:


```
title = "title here" 
template = "page.html"
date = "2017-07-16T19:20:30.45+01:00"
+++

hello, world.
```





## Jekyll Overview

### Built with Jekyll
Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through Markdown and Liquid converters, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server. Jekyll also happens to be the engine behind GitHub Pages, which means you can use Jekyll to host your project's page, blog, or website from GitHub's servers for free (taken from Jekyll's website: http://jekyllrb.com/docs/home/).

### Get your workstation set up
* Install <a href="www.ruby-lang.org/en/downloads">Ruby</a>
* Install <a href="rubygems.org/pages/download">RubyGems</a>
* Install <a href="nodejs.org">NodeJS</a>
* Install <a href="jekyllrb.com/docs/installation">Jekyll</a>

### Basic Usage (recommended)
In one terminal, build the jekyll site, watching for any changes (run in site root directory)
```
$  jekyll build --watch
```
In another terminal, start a local server (run in site root directory)
```
$  jekyll serve
```
View the site in your browser at
```
localhost:4000/template/
```


## File structure
```
|-- README.md (this)
|-- _config.yml (overall configuration file for the site)
|-- _includes (all the markup partials)
|   |-- footer.html
|   |-- head.html
|   |-- header.html
|-- _layouts (page markup templates)
|   |-- about.html
|   |-- contact.html
|   |-- main.html
|   |-- project.html
|   |-- reports.html
|-- _projects (markdown files that make up the "projects" jekyll collection)
|   |-- 2014-09-22-project-1.md
|   |-- 2014-09-23-project-2.md
|   |-- 2014-09-24-project-3.md
|   |-- 2014-09-25-project-4.md
|   |-- 2014-09-26-project-5.md
|   |-- 2014-09-27-project-6.md
|   |-- 2014-09-28-project-7.md
|   |-- 2014-09-29-project-8.md
|-- _site (the entire site after it is processed by Jekyll)
|   |-- README.md
|   |-- about
|   |-- contact
|   |-- feed.xml
|   |-- index.html
|   |-- projects
|   |-- reports
|   |-- public
|-- about.md (About Page in markdown)
|-- contact.md (Contact Page in markdown)
|-- feed.xml (General information about Jekyll's usage)
|-- index.html (Home Page of the Site)
|-- public (static content including fonts, images, js, and css files)
|   |-- fonts
|   |-- images
|   |-- javascripts
|   |-- stylesheets
```

## More on how Jekyll works

The \_site directory, contains no directories or files there begin with an underscore (\_). 
The contents of that directory are the end result of Jekyll's processing engine. 
(e.g.) jekyll build or bundle exec jekyll serve

One of the two commands that you need to run in order to host the site on a local server:
```
jekyll build --watch
``` 
-runs Jekyll engine, processing and reprocessing the "raw" files every time you make a change to a file
-you may exclude the --watch flag, if you do not want continuous delivery of your jekyll site

### Front Matter
Any file that contains a YAML front matter block will be processed by Jekyll as a special file. The front matter must be the first thing in the file and must take the form of valid YAML, set between triple-dashed lines (taken from Jekyll's documentation: http://jekyllrb.com/docs/frontmatter/). Here's a basic example that you'll find in the index.html file:
```
---
layout: default
title: Portfolio
---
```
This first item tells Jekyll to take all of the markup in index.html and plug it into the _layouts/main.html template to take the place of the {{ content }} variable found in that template file.
The second item tells Jekyll to create a variable, page.title, that you can use in the markup of the template. For example, in _layouts/main.html, you could write:
```
<head>
	<title>{{ page.title }}</title>
</head>
```
and that would render as:
```
<head>
	<title>Portfolio</title>
</head>
```

### Collections
Collections allow you to define a new type of document that can be somewhat conceptualized as an object type, each having its own unique properties and namespaces. These collections are declared in the _config.yml file:
```
collections:
  projects:
    output: true
    permalink: /projects/:path/
```
For this site, we only use one collections: projects, the contents of which can be found in the _projects directory. Notice that this directory name begins with an underscore. This is because each file in it only contains some combination of markdown and front-matter and will be processed by Jekyll's engine. Let's look at projects/2014-09-22-project-1.md as an example:
```
---
layout: project
title: Project 1
date: September 22, 2014
image: http://unsplash.it/400?random
---
/////////////////////////////////////

```
This file represents a project in the projects collection and contains both YAML front matter and Markdown. You can see how powerful collections are if we take a look at a snippet of index.html:
```
<ul id="portfolio-gallery">
    {% for project in site.projects %}
        <li>
            <a href="{{ site.baseurl }}{{ project.url }}">
                <img src="{{ project.image }}">
                <h2>{{ project.title }}</h2>
            </a>
        </li>
    {% endfor %}
</ul>
```
The ```{% %}``` tags represent liquid syntax and their contents are processed by Jekyll to render static HTML in the final site. You can see that all of the projects in the projects collection can be referenced with ```site.projects``` and iterated through with a for loop. In this specific for loop, for each project in the projects collection, we pull its image and title using ```{{ }}``` tags. All of a particular project's information is defined in its markdown file just like the one which we saw above. You can find more useful information about collections in Jekyll's website (http://jekyllrb.com/docs/collections/).


## Maintaining the Site

### Adding Projects
To add a project, just create a .md file in the _projects directory with front matter at the beginning that follows this format (taken from 2014-09-22-project-1.md):
```
---
layout: project
title: Project 1
date: September 22, 2014
image: http://unsplash.it/400?random
---
```
Following that front matter, just add content in regular markdown.


**References:**

Original Repository on GitHub(https://github.com/NU-MSR/msr-site)

Jekyll Official Website(http://jekyllrb.com/docs/home/)

Jekyll on GitHub(https://github.com/jekyll/jekyll)

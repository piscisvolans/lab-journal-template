Lab journal template
==================

This guide was written by Rebecca Holmes. Contact me at rholmes4@illinois.edu if you need help.

The template given here is a slightly modified version of [Poole](https://github.com/poole/poole). Thanks to the Poole developers! This repository aims to provide detailed instructions for set-up and use, not a totally orignal template.

*NOTE: I wrote this guide using Jekyll on Windows 7. Jekyll and the other tools needed to build this project are also available for Mac and Linux, but I don't have any experience using them on other platforms.*

## Table of Contents

* [Introduction](#introduction)
  * [What is Jekyll?](#what-is-jekyll)
* [Installation and setup](#installation-and-setup)
  * [Clone this GitHub repository](#clone-this-github-repository)
  * [Install Ruby and Jekyll](#install-ruby-and-jekyll)
  * [Install bibtex2html](#install-bibtex2html)
  * [Optional: Install Mendeley](#optional-install-mendeley)
* [Running Jekyll](#running-jekyll)
  * [Updating the live website](#updating-the-live-website)
  * [Hosting the site locally](#hosting-the-site-locally)

Introduction
------------------

This guide explains how to set up an online lab journal using a tool called Jekyll. You could also set up a lab journal on a blogging service like Wordpress or Blogger, which might look less complicated. Here are a few reasons to consider doing it with Jekyll:

1. You have complete control over the appearance and function of your lab journal website. This guide provides a basic template which you can customize any way you want.
2. All the files for your lab journal will be on your computer, so there will be no need to export them from a blogging service if you need to back up your entries or store them somewhere else. If you're an Illinois engineering student, you can also host your lab journal on your free webspace at http://web.engr.illinois.edu/~yournetid and add optional pasword protection.
3. You can learn about building and hosting websites!

Installation and setup
------------------

You must complete a few steps before you can start the lab journal project. Nothing in this guide requires advanced technical knowledge, but you should be able to install software and enter commands in the command prompt.

###Download the files in this GitHub repository

You can download all the necessary files in a .zip by clicking on "Download ZIP" in the sidebar to the right. Extract these files to the folder where you want to keep your lab journal--I keep mine on Dropbox so I can edit it from different computers.

###Install Ruby and Jekyll

Jekyll is based on the programming language Ruby. You don't need to know how to use Ruby, but it must be installed on your computer for Jekyll to work.

1. Install Ruby using [RubyInstaller](http://rubyinstaller.org/downloads/). Install the latest DevKit, available on the [RubyInstaller downloads page](http://rubyinstaller.org/downloads/).

2. After extracting the DevKit package, use the command prompt (type `cmd` in the Windows search bar) to `cd` to the folder where you extracted it (I'll call that folder ```my-lab-journal``` in this guide).  Run the following commands:

    ```
    ruby dk.rb init
    ruby dk.rb install
    ```

3. Install the RubyGem Jekyll by typing:

    ```
    gem install jekyll
    ```
    
4. Install the RubyGem RDiscount (a processor for Markdown, which we will use for simple text formatting):

    ```
    gem install rdiscount
    ```

###Install bibtex2html

bibtex2html is a program that converts BibTeX files to HTML so a list of references can be displayed on a webpage. Jekyll uses it to process the BibTeX file ```publications_web.bib``` in the ```_bibliography``` directory. If it is not installed or installed in the wrong location, Jekyll will give an error when you try to run it, and the list of publications will not be generated.

*If for some reason you are unable to successfully run Jekyll with bibtex2html, it is possible to disable this feature and leave the current list of publications. See [Managing publications](#managing-publications).*

1. Install bibtex2html from the [bibtex2html home page](https://www.lri.fr/~filliatr/bibtex2html/). Use the Windows 1.95 installer. Put it in ```C:/Bibtex2html/bibtex2html.exe``` or Jekyll won't be able to use it. (This can be changed by editing ```bibjekyll.rb``` in the ```_plugins``` directory under the comment "call bibtex2html", but you will probably make someone else unhappy by changing it.)

###Optional: Install Mendeley

[Mendeley](http://www.mendeley.com/) is an academic reference manager. I use it to organize the citations that appear on the Publications page of the website. If you follow a few steps, you can use Mendeley, plus a simple Python script and Jekyll's interface with bibtex2html to maintain the list of citations, including automatically linking to the DOI and to a hosted .pdf file if one is available. Details are in [Managing publications](#managing-publications).

If you don't need to add, remove, or edit the content of citations, you don't need to install Mendeley or make any changes to ```publications_web.bib```. You can change certain formatting options (such as how the author names are abbreviated) in the ```style.bst``` file that bibtex2html uses.

Running Jekyll
------------------
If you've just copied the website files from GitHub to a new computer and you and haven't run Jekyll yet, the ```_site``` directory in your repository should be empty. When you run Jekyll, ```_site``` is where all the assembled pieces of the website will go--the finished product. GitHub will not sync the files in ```_site```. You can always generate them again by running Jekyll.

To run Jekyll and fill the empty ```_site``` directory with the assembled website, use the command prompt to ```cd``` to ```group-website-jekyll```. Then just enter the command

```
jekyll build
```

That's it! The ```_site``` directory should now be populated with the website files. The live website at http://research.physics.illinois.edu/QI/Photonics/ has not been updated, though.

###Updating the live website
After running Jekyll, just replace the contents of ```Photonics``` with the entire contents of ```_site```. You can do this in Windows Explorer if you have access to the networked folder where our webspace is, or you can use SSH. Contact help@physics.illinois.edu if you need help acccessing the webspace.

###Hosting the site locally

If you're testing out changes, it can be useful to tell Jekyll host the website on your own computer so you can view it in a browser exactly as it will appear when it goes live. I recommend previewing all changes this way.

It can also be nice to set Jekyll to automatically rebuild the site when you make changes. To do both of these things, you need to make a small change to the ```_config.yml``` file, and type an extra option when you run Jekyll. First, open ```_config.yml``` and change ```baseurl``` to "", like this:

```
url: "http://research.physics.illinois.edu/QI/Photonics"
baseurl: ""
```

Save the file. Now when you run Jekyll, use the ```server``` command with ```--watch```:

```
jekyll server --watch
```

This tells Jekyll to build the website, to host the contents of ```_site``` locally, and to automatically rebuild if you change anything. Now you should see the website if you point your browser to http://localhost:4000. (Reminder: what you see are still just files on your computer--you need to copy them to our webspace to make any changes live.) 

Change ```baseurl``` back to ```/QI/Photonics``` and run ```jekyll build``` one more time when you're ready to upload your changes, or all the links that use the ```{{ site.baseurl }}``` variable will be broken. (The purpose of ```baseurl``` is to account for the ```/QI/Photonics``` in the URL of the live website. Those folders aren't there when you host locally, so you need to tell Jekyll not to insert them in internal URLs.)

A brief description of how Jekyll works
------------------

If you just want to know how to update a specific part of the website (like adding a news post), scroll down past this section to [How to do specific tasks](#how-to-do-specific-tasks). If you want an overview of what Jekyll is doing when you run it, read on.

Take a look at the list of files and folders in the group-website-jekyll repository. When you run Jekyll, it looks through all those files and folders, and follows certain rules to assemble the pieces they contain into a finished website in the ```_site``` directory. These are the main types of files and folders Jekyll looks at (for more details, see http://jekyllrb.com/docs/structure/):

1. Folders with no ```_``` (underscore) before their names. Jekyll just copies these directly to ```_site``` without changing anything. Example: ```img```, which contains all the images used on the website. ```css``` contains the CSS stylesheets for the website, which can be edited just like regular CSS. Files with no ```_``` and no [YAML frontmatter](#yaml-frontmatter) (I'll explain what this is soon) will also be copied to ```_site``` verbatim.

2. HTML files with no ```_``` before their names that also contain [YAML frontmatter](#yaml-frontmatter). Example: ```people.html```, the page with information about the people in our group. Jekyll processes each of these to create an HTML file in ```_site```. With current settings, ```people.html``` ends up in ```_site/people/index.html```. (```index.html```, the home page of the website, just goes to ```_site``` with no subfolder.)

3. Folders with ```_``` before their names. These folders are not copied to ```_site``` directly, but contain content and information that Jekyll uses to assemble the website. Examples:
    * ```_layouts``` contains HTML files which define page layouts that can be reused for many pages. For example,       ```_layouts/default.html``` is a layout which puts a navbar at the top of the page and a footer at the bottom, and also includes some CSS and Javascript that is used on most pages in the website.
    * ```_includes``` contains pieces of content which can be inserted into pages with a special command. For example, ```{% include navbar.html %}``` will insert the code for a navbar wherever Jekyll finds it. ```{% markdown aboutus.md %}``` will process and insert the Markdown text in ```aboutus.md```, which appears under "About us" on the front page of the website. (More about Markdown later.)
    * ```_data``` contains YAML files with well-formatted data that Jekyll can use. For example, ```group_members.yml``` contains a list of current group members, their email addresses, and the filenames of headshot images. Jekyll uses it to generate the final People page.
    * ```_plugins``` contains Ruby scripts which give Jekyll extra features. For example, ```bibjekyll.rb``` handles the list of citations on the Publications page.
   
4. ```_config.yml``` is a special file which contains Jekyll's configuration information. You probably don't need to edit it unless you want to host the site locally (see [Hosting the Site Locally](#hosting-the-site-locally), above).

###YAML frontmatter

YAML frontmatter is information contained between two lines of ```---``` at the start of a file, like this example from ```people.html```:

```
---
layout: default
title: People
---

<h1 style="text-align:center">Our group</h1>
<div class="people">

	{% include group-members.html %}

	<h1 class="category-title">Previous group members</h1>
	
	{% include previous-group-members.html %}
	
</div>
```

The YAML frontmatter gives Jekyll information and instructions when processing the file that contains it. The ```layout``` variable tells Jekyll which of the layouts in ```_layouts``` it should use for this page--in this example, the People page will use the default layout in ```_layouts/default.html```. The ```title``` variable tells Jekyll the title of the page. These variables can be accessed elsewhere on the website. For example, ```default.html``` automatically sets the title of each page to ```page.title```, and the navbar uses ```page.title``` to decide which page is the current page and highlight its link.

Jekyll will *only* process HTML documents in the main directory if they have YAML frontmatter. In other contexts, it is optional. Read more about YAML in the Jekyll documentation: http://jekyllrb.com/docs/frontmatter/.

###Markdown

Markdown is a text-to-HTML tool. It allows you to write good-looking content for the web without using HTML tags. Markdown files look more like regular text files, which makes them easier to read and work with. Markdown processes ```.md``` files to insert all the ugly HTML tags that make text display properly on the web.

Most of the text content for the group website is in Markdown files in the ```_includes``` directory.

* This is a useful Markdown cheat sheet: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

* And here's an online Markdown editor you can use in your browser: http://dillinger.io/

Markdown will also process many HTML tags, if you need to sneak some in there.

###Liquid
Jekyll uses the [Liquid templating language](http://liquidmarkup.org/}) to handle variables, some logic operations, and to enable "including" files in other files. All the tags you see with ```{ }``` or ```{{ }}``` are Liquid tags. 

* This is a good introduction to using Liquid: http://docs.shopify.com/themes/liquid-basics

A few examples of how Liquid is used for the Kwiat group website:

* In the default layout ```default.html```, the variable ```page.title``` is used to make the ```<title>``` of each page match the title specified in its YAML frontmatter:
    ```
    <title>Kwiat Quantum Information Group: {{ page.title }}</title>
    ```

* For almost all images on the site, the path to the image is specified using the ```site.url``` variable, which is set in ```_config.yml```. If you ever need to change the site url, all the image paths will still be correct. This way of specifying the path is also used for CSS and Javascript, and for files in the ```theses``` and ```papers``` directories
    ```
    <img src="{{ site.url }}/img/physrev-2013.jpg" class="movie-still">
    ```
* Liquid is used to do loops and logic operations in a few places on the site, including on the People page. This code renders the names and pictures of graduate students, automatically organizing them in rows of three columns each and adding new rows if needed:

    ```
<h1 class="category-title">Graduate Students</h1>
{% for category in site.data.group_members %} <!-- Displays students with 3 students to a row, adding new rows if needed-->
		{% if category.name == "Graduate Students" %}
			{% assign count = 0 %} <!-- Initialize variable that counts to 3 -->
			{% for person in category.people %}
			
				{% assign count = count | plus: 1 %} <!-- Increment -->
				
				{% if forloop.first %} <!-- If this is the first item, start a row -->
					<div class="row row-centered">
				{% else %}
				{% endif %}

				<div class="col-md-4 col-centered">
					<a href="http://physics.illinois.edu/people/profile.asp?{{ person.netid }}">
					<div class="thumbnail">
						<img src="{{ person.image }}" class="img-circle">
						<div class="caption"><h2>{{ person.name }}</h2>
						<h5 class="email">{{ person.netid }}@illinois.edu</h5>
						</div>				
					</div>
					</a>
				</div>
				
				{% if count >= 3 and forloop.last == false %} <!-- If we've reached a multiple of 3, end this row and start a new one, unless this is the last item -->
					</div>
					<div class="row row-centered">
					{% assign count = 0 %} <!-- Rest the count -->
				{% elsif forloop.last %}
					</div> <!-- End the row if this is the last item -->
				{% endif %}

			{% endfor %}
		{% else %}
		{% endif %}
{% endfor %}
    ```

How to do specific tasks
------------------

Okay, you installed this stupid Jekyll thing and now you just want to be able to add a news post or delete a recently-graduated group member. This section will hopefully cover most common maintanence tasks.

###Adding a news post

Create a new [Markdown](#markdown) file. Give it some [YAML frontmatter](#yaml-frontmatter) (see the previous section) and add your content below, as in this example:

```
---
title: Students awarded NSF Graduate Research Fellowship and Goldwater Scholarship
layout: default
image: nsf1.gif
---

Second-year graduate student [Courtney Byard](http://physics.illinois.edu/news/story.asp?id=2470) received a 2013 Graduate Research Fellowship from the National Science Foundation. Rising senior undergraduate [David Schmid](http://physics.illinois.edu/news/story.asp?id=2417) received a 2013 Barry M. Goldwater Scholarship. Second-year graduate student Rebecca Holmes also received an NSF fellowship in 2012.
<!--more-->
```

```title``` should be the title of your news item, ```layout``` can stay "default," and ```image``` should be the filename of a small image you want to place next to your news item. Put the image in ```img```. The ```.newsbox img``` class in ```group.css``` currently resizes images to 75x75 px.

If your news post is longer than a few sentences, place the excerpt separator ```<!--more-->``` where you want the news post to break off on the home page of the website. Continue your text after the separator. In the YAML frontmatter, add the line

```
more: "yes"
```

This will tell Jekyll to add a "More" link at the end of your post excerpt on the main page, which will direct the reader to the full post on the News page.

Save your file in ```_posts``` as ```YEAR-MONTH-DAY-title.md```. For the example above, the filename should be ```2013-04-02-students-awarded-nsf-graduate-research-fellowships.md```. (Only the month and year will actually be displayed, although the day will be used to order posts.)

Run Jekyll, and your new post should appear on the main page and on the News page! Currently the main page is set to display only the three most recent news posts. If you want to change that limit, edit ```_includes/newsbox.html``` where it says ```{% for post in site.posts limit: 3 %}```.

###Changing information about group members

Jekyll generates the content of the People page using information from two files in the ```_data``` directory: ```group_members.yml``` and ```previous_group_members.yml```. These data files are processed in two HTML files, ```group-members.html``` and ```previous-group-members.html```, which are both included in ```people.html```. (You can see the include commands in the example in the [YAML frontmatter](#yaml-frontmatter) subsection above.)

To add, remove, or change the information about a current group member, just edit his or her entry in ```group_members.yml```. For example, adding the following under the "Graduate Students" category...

```
- name: "Graduate Students"
  people:
    - name: "Smarty McSmartypants"
      image: "../img/headshot_blank.jpg"
      email: "smarty2@illinois.edu"
```

...will add a new person under the Graduate Students heading on the People page, complete with headshot and email address. Notice that different categories of people have different options--if you add an email address for a person in the "Undergraduate Students" category, it won't show up on the People page because ```group-members.html``` doesn't display email addresses for undergrads (unless you alter it so that it does!) The current settings also automatically organize graduate and undergraduate students in rows with three columns each. You can change this in ```group-members.html```.

That's basically it. Be sure to follow the existing YAML formatting exactly, because extra spaces or line breaks will cause errors. **Important: there must not be any tab characters in YAML files. Your text editor may add them automatically! Indentation is an important element of YAML syntax, and all the blank characters must be spaces, not tabs. Or things will break.**

Similarly, to add, remove or change the information about a past group member, edit his or her entry in ```previous_group_members.yml```, like so:

```
- name: "Graduate Students"
  people:
    - name: "Best grad student ever"
      year: "1957"
      thesis-type: "phd"
      thesis-file: "best-thesis.pdf"
      thesis-title: "Really Great Thesis"
      currently: "Retired"
      past: "Won a Nobel prize in every field"
```

Follow the existing examples. In the "Postdocs" and "Graduate Students" categories, most of the extra information (thesis, currently, past) is optional. Thesis files should go in the ```theses``` directory and have the filename specified.

###Adding a new page and editing the navbar

To add a new page to the site, create a new HTML or [Markdown](#markdown) file in the group-website-jekyll repository. Give it some [YAML Frontmatter](#yaml-frontmatter) specifying, at minimum, a title and layout. Add your content below the frontmatter. That's it--the next time you run Jekyll, it will create your page as ```_site/newpagename/index.html```. If for some reason you prefer not to process your new page with Jekyll, leave out the YAML frontmatter. The HTML file will be copied as-is to the ```_site``` directory.

The navbar element is generated with ```navbar.html```, which is included in the main layouts for website pages. The navbar includes the file ```pages_list```, which looks through the data file ```navbar_links``` and adds links to the navbar in the order they appear. To add a new link, just add a new entry in ```navbar_links.yml```. For example, this entry tells the navbar to include a link called "People" which points to the directory "people" under the main site url:

```
- name: "People"
  url: "people/"
```

It appears second in the list of links, after "Home," so it will appear in the second position on the navbar.

If an item in ```navbar_links.yml``` has child links (like Research does), they are organized in a dropdown menu. Child links are basically a table of contents--they point to an tag on the parent page with the ```id``` equal to the handleized (spaces and special characters replaced with dashes) name of the child link. The exception is if the child link specifies a url, in which case its item in the dropdown menu will point to that url. For example:

```
- name: "Research"
  url: "research/"
  child_links:
    - name: "Guide to Quantum State Tomography"
      url: "Tomography/"
      divider: ""
      highlight: "yes"
    - name: "Tests of Nonlocality"
      header: "Fundamental Studies"
    - name: "Multipartite Entanglement"
      divider: ""
```

The first child link specifies a url, so it will point to a separate page. The second two child links do not specify urls, so they will point to the locations on the Research page identified by ```tests-of-nonlocality``` and ```multipartite-entanglement```, respectively.

###Managing research topics

To reduce the number of things you need to change when adding or removing a research topic, or changing the order of existing topics, several elements of the website are linked together. The data file ```navbar_links.yml``` (see the [previous section](#adding-a-new-page-and-editing-the-navbar)) contains a list of child links under the "Research" element. ```research.html``` includes the file ```topics_list```, which goes through these child links, looks for a Markdown document for each of them, and renders the content on the final Research page.

####Editing the content of an existing topic
The content (text and images) for each topic on the Research page is contained in a separate Markdown file in the ```_includes``` directory. To edit the content of a topic, just edit its Markdown file.

####Changing the order of existing topics
To change the order of existing topics, rearrange them in ```navbar_links.yml```. You can change the locations of headers and dividers to organize the topics--follow the existing examples. The Research page and the dropdown menu in the navbar will both reflect your changes.

####Removing a topic
To remove a topic, delete its child link from ```navbar_links.yml```. It will no longer appear on the Research page or in the navbar dropdown menu. You can also delete the Markdown file for that topic if you want to remove it permanently.

####Adding a new topic
To add a new topic, add a new child link in the location where you want the topic to appear, and create a [Markdown](#markdown) file with content. The next time you run Jekyll, the new topic will appear on the Research page and in the dropdown menu. For this to work properly, you must follow a specific naming convention in ```navbar_links.yml``` and in the Markdown file:

* The name of the child link in ```navbar_links.yml``` must be the title of the topic, exactly as you want it to appear in the dropdown menu and on the Research page
* The Markdown file for that topic must be in the ```_includes``` directory and have the filename equal to the handleized name of the child link

For example, the child link with the name "Quantum Random Number Generation" corresponds to a Markdown file called ```quantum-random-number-generation.md```.

###Managing Publications

Jekyll generates the list of citation on the Publications page with the help of a Ruby program in the ```_plugins``` directory called ```bibjekyll.rb```. This plugin is invoked with a special tag in ```publications.html```: ```{% bibtex _plugins/style _bibliography/publications_web.bib %}```. This tells ```bibjekyll.rb``` to process the BibTex file ```_bibliography/publications_web.bib``` using the BibTeX style in ```_plugins/style.bst``` and render the result as HTML. The actual BibTeX to HTML conversion is done with the program bibtex2html, which must be installed on your computer (see [Installation and setup](#installation-and-setup)).

To begin managing the list of citations that appears on the Publications page, I recommend you install [Mendeley](http://www.mendeley.com/). Contact me (Rebecca Holmes, rholmes4@illinois.edu) and I will give you my Mendeley login information so you can access the folder "Group website." This folder contains all the citations which appear on the website. Download all the .pdf files that are available.

Below is the basic outline of what you should do to update the list of citations. It's a little complicated, but it's designed to automate the process of linking to .pdf files, if they are available, and copying those .pdf files to the group-website-jekyll repository so they will be available on the website. 

1. Make sure all the citations you want to include are in the "Group website" folder in Mendeley, and that all their information is correct. Make sure all the existing document files are renamed to Title.pdf with the hyphen-separated option. (You can do this in Mendeley by going to File --> Rename Document Files.)

2. Select all the citations in "Group website" and go to File --> Export. Export as Endnote XML to the ```papers``` directory in the group-website-jekyll respository. This will copy all the .pdf files for the citations to ```papers/My Collection.Data/PDF```.

3. Select all the citations again and go to File --> Export. This time export as a BibTex file called ```publications.bib``` in the ```_bibliography``` directory.

4. The way Mendeley exports the filename of .pdf documents in each citation is not ideal. To fix it, run the Python script ```bibfile.py``` in the ```_bibliography``` directory. It requires installing the package bibtexparser. If you have Python 3 and pip installed on your computer, all you need to do is run the command:
    ```
    pip bibtexparser
    ```
And then, in the ```_bibliography``` directory:
    ```
    python bibfile.py
    ```
The script will create a new file called ```publications_web.bib```.

5. Run Jekyll. Your changes should show up on the Publications page.


####Bypassing publications management
If you can't or don't want to manage the list of citations this way, you don't have to, but it will be difficult to go back once you start editing ```publications_web.bib``` manually. To make manual changes, edit ```publications_web.bib``` directly, making sure that "file" elements have the correct path for .pdfs you want to link to.

You can also completely disable Jekyll's processing of publications, and make the website simply use a static HTML file containing the citations. To do this, look in the ```_site``` directory for the file ```publications_web.html```. Copy this file to the ```_includes``` directory. In ```publications.html```, replace the tag ```{% bibtex _plugins/style _bibliography/publications_web.bib %}``` with ```{% include publications_web.html %}```. Jekyll will no longer call ```bibjekyll.rb```. You will need to reverse this change if you ever want to enable dynamic generation of the citations list.

Troubleshooting
-----------------

###Coming soon?
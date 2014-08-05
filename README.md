Lab journal template
==================

This guide was written by Rebecca Holmes. Contact me at rholmes4@illinois.edu if you need help.

The template given here is a slightly modified version of [Poole](https://github.com/poole/poole). Thanks to the Poole developers! This repository aims to provide detailed instructions for set-up and use, not an orignal template.

*NOTE: I wrote this guide using Jekyll on Windows 7. Jekyll and the other tools needed to build this project are also available for Mac and Linux, but I don't have any experience using them on other platforms.*

## Table of Contents

* [Introduction](#introduction)
  * [What is Jekyll?](#what-is-jekyll)
* [Installation and setup](#installation-and-setup)
  * [Download the files in this GitHub directory](#download-the-files-in-this-github-repository)
  * [Install Ruby and Jekyll](#install-ruby-and-jekyll)
* [Running Jekyll](#running-jekyll)
  * [Hosting your lab journal locally](#hosting-your-lab-journal-locally)
* [Writing and editing entries](#writing-and-editing-entries)

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

Running Jekyll
------------------
If you've just downloaded the project files from GitHub and you and haven't run Jekyll yet, the ```_site``` directory in ```my-lab-journal``` should be empty. When you run Jekyll, ```_site``` is where all the assembled pieces of the website will go--the finished product. You shouldn't edit the files in ```_site```, because they will be overwritten every time you run Jekyll. To make changes, you'll edit files in ```my-lab-journal``` and Jekyll will update the website for you.

To run Jekyll and fill the empty ```_site``` directory with the assembled website, use the command prompt to ```cd``` to ```my-lab-journal```. Then just enter the command

```
jekyll build
```

That's it! The ```_site``` directory should now be populated with the website files. 

###Hosting your lab journal locally

To view your lab journal the way it will look in a browser, you can tell Jekyll to host it from your computer. You can also turn on automatic updates, so Jekyll will automatically rebuild the site whenever you make changes. To do both of these things, run Jekyll using the ```server``` command with ```--watch```:

```
jekyll server --watch
```

Now you should see the lab journal template if you point your browser to http://localhost:4000.


Writing and editing entries
--------------------------

Jekyll uses Markdown, a way of formatting text for the web without using HTML tags. To take advantage of this, I suggest using a Markdown editor to write and edit your entries. This is easiest if your lab journal files are on Dropbox. If they are, go to http://dillinger.io and click on "Dropbox." Select "Link with Dropbox," then "Import from Dropbox." Import the file ```2014-08-01-example-content.md``` in ```my-lab-journal/_posts```.

If you lab journal files are not on Dropbox, you can open ```2014-08-01-example-content.md``` with a a text editor (I recommend [Notepad++](http://notepad-plus-plus.org/)).

```2014-08-01-example-content.md``` contains some examples of how you can use Markdown and HTML tags to format your text and to insert images and links. If you followed the steps in [Hosting your lab journal locally](#hosting-your-lab-journal-locally) above, Jekyll should automatically implement any changes--try adding some text to ```2014-08-01-example-content.md```, save the file (on Dillinger, do this under the "Dropbox" menu), refresh the page in your browswer, and see if the changes appear.

Now try making a new entry. All new entries should follow these steps:

1. Create a new file. At the very top, put the lines
    ```
    ---
    layout: post
    title: Example content
    ---
    ```
Change the "title" to the title of your new entry, and leave the layout as "post."

2. Save the file in ```_posts``` as ```YYYY-MM-DD-your-post-title.md```. It's important to format the file name this way, because it tells Jekyll the date for your post.
3. Write your entry below the lines in step 1.

###Markdown

Markdown is a text-to-HTML tool. It allows you to write good-looking content for the web without using HTML tags. Markdown files look more like regular text files, which makes them easier to read and work with. Markdown processes ```.md``` files to insert all the ugly HTML tags that make text display properly on the web.

Most of the text content for the group website is in Markdown files in the ```_includes``` directory.

* This is a useful Markdown cheat sheet: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

* And here's an online Markdown editor you can use in your browser: http://dillinger.io/

Markdown will also process many HTML tags, if you need to sneak some in there.
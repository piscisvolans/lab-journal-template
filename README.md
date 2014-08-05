Lab journal template
==================

This guide was written by Rebecca Holmes. Contact me at rholmes4@illinois.edu if you need help.

The template given here is a slightly modified version of [Poole](https://github.com/poole/poole). Thanks to the Poole developers! This repository aims to provide detailed instructions for set-up and use, not an orignal template.

*NOTE: I wrote this guide using Jekyll on Windows 7. Jekyll and the other tools needed to build this project are also available for Mac and Linux, but I don't have any experience using them on other platforms.*

## Table of Contents

* [Introduction](#introduction)
* [Installation and setup](#installation-and-setup)
  * [Download the files in this GitHub directory](#download-the-files-in-this-github-repository)
  * [Install Ruby and Jekyll](#install-ruby-and-jekyll)
* [Running Jekyll](#running-jekyll)
  * [Hosting your lab journal locally](#hosting-your-lab-journal-locally)
* [Writing and editing entries](#writing-and-editing-entries)
  * [More about Markdown](#more-about-markdown)
* [Hosting your lab journal on the College of Engineering webspace](#hosting-your-lab-journal-on-the-college-of-engineering-webspace)

Introduction
------------------

This guide explains how to set up an online lab journal using a tool called Jekyll. You could also set up a lab journal on a blogging service like Wordpress or Blogger, which might seem less complicated. Here are a few reasons to consider doing it with Jekyll:

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

Now you should see the lab journal template if you point your browser to http://localhost:4000. You can use your lab journal this way if you want to--or you can [upload it to your College of Engineering webspace](#hosting-your-lab-journal-on-the-college-of-engineering-webspace).


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

As soon as the file for your new entry is saved in ```_posts```, it should show up on the locally hosted version of your lab journal (or the next time you run ```jekyll build``` if you're not hosting locally).

###More about Markdown

Markdown is a text-to-HTML tool. It allows you to write good-looking content for the web without using HTML tags. Markdown files look more like regular text files, which makes them easier to read and work with.

* This is a useful Markdown cheat sheet: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

Markdown will also process many HTML tags, if you need to sneak some in there (to insert images, for example).

Hosting your lab journal on the College of Engineering webspace
---------------------------------------------------------------------

If you're a College of Engineering student (which, if you're a physics graduate or undergraduate student, you are) you already have an Engineering Workstation account and some free webspace. To access it, go to https://web.engr.illinois.edu and log in with your NetID and AD password.

Under "Files," you can click on "File Manager" to see the files and folders in your webspace. If there's an ```index.html``` in the ```public_html``` folder, it will show up when you go to http://web.engr.illinois.edu/~yournetid/.

To upload your lab journal, it's easier to access your webspace with SSH. Download and install [WinSCP](http://winscp.net/). Log in with the following:
* Host name: web.engr.illinois.edu
* User name: Your NetID
* Password: Your AD password

After logging in, you should see your local files on the left and the files on your webspace to the right. Navigate to your local ```my-lab-journal``` folder, select everything in the ```_site``` folder, and drag it over to the ```public_html``` folder on your webspace. You'll do this every time you update your lab journal--maybe sure to select and copy everything, and choose "yes" if WinSCP asks if you want to overwrite existing files.

Your lab journal should now be live at http://web.engr.illinois.edu/~yournetid/ !

You might want to set a password to restrict access to your lab journal. You can do this easily by clicking on "Password protect directories" under "Security" on the main page at https://web.engr.illinois.edu. Just follow the instructions to add authorized users and corresponding passwords. (Choose the entire ```public_html``` folder as the directory to password protect.)

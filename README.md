# The UW Energy Electrochem Nexus main website

Our website, http://UW-EEN.github.io, is a [GitHub Pages](https://pages.github.com/) site built with [Jekyll](https://jekyllrb.com/) and [Bootstrap](http://getboostrap.com), originally pulled from [D. Allan Drummond's site](https://github.com/drummondlab/drummondlab.github.io) which in turn was pulled from [Trevor Bedford's site](http://bedford.io) and heavily modified.
Our site will essentially copy their format and incorporate minor changes as we start to learn some website development. Go [here](http://drummondlab.org/about.html) to find more details about the template design.

# Editing the site

Here's a step-by-step guide to making modifications to the site, focused initially on adding typical content. You'll need a working Unix-like environment and working knowledge of Git, [Markdown](https://daringfireball.net/projects/markdown/syntax), HTML, and Unix commands. 
You'll need a working Ruby installation, with gems for Jekyll, GitHub Pages, and their dependencies installed. For now, if you need help getting set up, ask someone who's already up and running.

## Installing requirements

You will need a working Ruby installation, with gems for Jekyll, GitHub Pages, and their dependencies. Start by finding the [Ruby installer](https://www.ruby-lang.org/en/downloads/) for your OS and
install Ruby using default settings (press enter when it asks if you are unsure).

Then follow instructions for [installing Jekyll](https://jekyllrb.com/docs/installation/) for your OS.
 Use the default options in the Ruby installer.

    jekyll -v
    bundler -v

This should output something like:

    jekyll 4.0.0
    Bundler version 2.1.4

Then make sure the Gemfile in the root directory contains the line `gem 'github-pages', group: :jekyll_plugins` and run:

    bundle install

If you didn't receive any errors, you should be ready to start contributing!


## Clone the repository

If you're a member of the [Energy Electrochem Nexus team](https://github.com/orgs/Energy-Electrochem-Nexus/people), you have access to the website repository.

To clone the repository, making a local copy on your machine:

	git clone https://github.com/Energy-Electrochem-Nexus/Energy-Electrochem-Nexus.github.io

Enter your local repository and check out the `staging` branch, where you'll make changes before promoting them to the `master` branch and publishing them:

	cd Energy-Electrochem-Nexus.github.io
	git checkout staging

## How to commit files to GitHub

If you have cloned a copy of the repository on your machine, you might also want to make changes or additions to files and commit them to the main branch. 
General steps to commit files to GitHub can be found below, as well as few additional ones that willallow for oushing files to the main branch for this website. 

    git status
    git add + file
    git commit -m " add commit message to be displayed on GitHub

Before you can complete the commit you will also have to run the following commands:

    git remote set-url origin https://github.com/UW-EEN/UW-EEN.github.io.git
	[the step above will beed to be run only the first time]
    git fetch origin
    git rebase origin/staging
    git push


## Overview of the structure

Let's assume you're familiar with HTML pages. A site is a collection of HTML pages. For our site (and many others), there are page types, like a paper page, or a lab member page, which are the same in design but different in content. In the web-accessible site, these are indeed different pages. However, as you might hope, they are _generated_ from a single template file filled in with information from many paper- or member-specific data files. This generation is done every time the site changes; it's handled by GitHub Pages, the service we use.

The template files are weird-looking HTML files residing in the `_includes/themes/lab` folder.

## How to add content

For most common actions---adding a lab member, paper, protocol, or news item---you'll be making a new Markdown file in the proper location, naming it properly, and filling in the required fields. In almost all cases, you can (and should!) copy an existing item, change the name, and change its content, rather than trying to write a Markdown document from scratch.

For example, suppose you want to add a news item, which will appear on the front page, announcing that you have created a yeast strain capable of secreting high-quality chardonnay. Go into the `news/_posts` folder. Copy one of the existing items into a new file named with today's date (it matters!) and a brief title:

	cp 2017-10-7-bg-jmw-ecs-232nd.md 2019-12-10-stu-flipped-class.md

The date is used by the generator; it's inelegant and perhaps there's a way to do it differently, but that's how it is for now. Now edit the new file to make the content what you want. Just open it in your favorite editor and type away. By the time you're done, hopefully you have something like this:

	---
    layout: news
    title: "Turning a New Leaf on Traditional Lectures"
    author: "Brian Gerwe"
    author_handle: "Brian"
    image: /assets/images/news/default-news.png
    category: news
    published: true
    tags: [teaching]
    ---
    [Stu][1] was featured in a ChemE department [article] about teaching the introductory thermodynamics class as a "flipped classroom".

    [1]: team/stu-adler
    [article]: https://www.cheme.washington.edu/news/article/2020-02-13/flipped-classroom

Now add it to the repository:

	git add 2019-12-10-stu-flipped-class.md

And, when you're happy with it, commit and push:

	git commit -m "Stu featured article"
	git push

This new announcement won't yet be public. The next section shows you how to do that.

The same basic process is used to add protocols, team members, etc.

## Updating the public site

All edits should be made on the `staging` branch. When you start work, make sure you're on the staging branch:

	git checkout staging

Once your edits are done, preview the site. Generate the pages and start the private webserver:

	rake preview

...and then open the local test site, http://127.0.0.1:4000. Look at anything you've changed and make sure it's good to go.

Then move the changes to the `master` branch:

	git checkout master
	git merge staging

and push to GitHub:

	git push

Changes won't be immediate, so wait a minute or two while GitHub's servers regenerate the site and publish it. Check to make sure the public site http://Energy-Electrochem-Nexus.github.io looks the way you intend.

Finally, check out `staging` again so that you don't accidentally start working on the `master` branch the next time you sit down:

	git checkout staging

## Changing look and feel

Fonts, colors, spacing, and similar stylings are separate from the template pages. Like most sites, we use Cascading Style Sheets (CSS), 

### To-dos

See Issues on [the site](https://github.com/Energy-Electrochem-Nexus/Energy-Electrochem-Nexus.github.io).


## License

[MIT](http://opensource.org/licenses/MIT)

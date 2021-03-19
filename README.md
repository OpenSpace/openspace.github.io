
# About

The source files for the [http://wiki.openspaceproject.com](http://wiki.openspaceproject.com) wiki page for the OpenSpace project.

This project uses [Jekyll](https://jekyllrb.com/) and the theme [Just the Docs](https://pmarsceill.github.io/just-the-docs/) to build and style the wiki. 

# Structure / Development

 - The wiki is devided by category based on who is using it. docs/developers, docs/builders, and docs/users.
 - Pages specific to certain modules/data are in docs/components/ these should be considered for rework.
 - Custom CSS rules can be put in \_sass/custom/custom.scss but should be used sparingly as they may affect other pages.


# Building locally:

- Install Ruby (on windows, I downloaded [RubyInstaller for Windows](https://rubyinstaller.org/) last tested with version 2.7.2)
- Install Jekyll (as per the [Jekyll site](https://jekyllrb.com/docs/) I installed the gems I needed `gem install jekyll bundler`)

- Clone Repository

- Install the ruby packages with  `$ bundle install`

- Run the server locally with `$ bundle exec jekyll serve`

- Access the site at [http://127.0.0.1:4000](http://127.0.0.1:4000)
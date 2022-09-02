# Personal Website

This is a simple personal material website (adopting HCZ theme).

## HCZ Material Theme Feature

* Sitemap and XML Feed
* Site Search 
* Projects and tags
* Paginations in homepage
* Posts under category
* Related Posts
* Highlight pre
* Next & Previous Post
* Disqus comment

#### Screenshot Sample

![Screenshot Home Page](https://raw.githubusercontent.com/ashutosh2k12/jekyllthemes/master/thumbnails/hcz-material.png  "Screenshot Home Page")

## Building the website

This website is building on the [Jekyll](https://jekyllrb.com/docs/usage/) gem. Typically you'll use jekyll serve while developing locally and jekyll build when you need to generate the site for production.

### Install and local deploy

Installing Jekyll

```console
foo@bar:~$ gem install bundler jekyll
```

Local deploy

```console
foo@bar:~$  git clone git@github.com:hbgit/hbgit.github.io.git
foo@bar:~$  cd hbgit.github.io.git
foo@bar:~$  sudo apt-get install ruby-dev
foo@bar:~$  bundle add webrick
foo@bar:~$  bundle install
foo@bar:~$  bundle exec jekyll serve
```

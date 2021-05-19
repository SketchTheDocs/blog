# Under The Hood

This website is built using the [Hugo](https://gohugo.io) static site generator and hosted at the [GitHub Pages endpoint](http://sketchthedocs.dev/blog) for this repo. I used the [Quickstart](https://gohugo.io/getting-started/quick-start/) guide to get started and chose the [hugo-clarity theme](https://github.com/chipzoller/hugo-clarity) for this purpose.

Here are the steps followed:

---

`STEP 1`:  install hugo for development.

```
$ brew install hugo
$ hugo version
hugo v0.83.0+extended darwin/amd64 BuildDate=unknown
```
---

`STEP 2`: Create a new hugo project (source directory)

```
$ hugo new site www
```

---


`STEP 3`: Add A Theme

Follow [chosen theme's directions](https://github.com/chipzoller/hugo-clarity#getting-up-and-running) to setup default configuration (non-customized). 

```
$ cd www
$ git submodule add https://github.com/chipzoller/hugo-clarity themes/hugo-clarity
$ cp -a themes/hugo-clarity/exampleSite/* .
```

Run server from www/ to verify theme works:

```
$ hugo server -D
..
..
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

---

`STEP 4`: Customize Theme

First, edit the `www/config.toml` to specify the baseURL for project

```
baseURL = "https://sketchthedocs.dev/blog/"
languageCode = "en-us"
title = "Sketch The Docs"
theme = "newsroom"
```

Then, look at that theme's [configuration guidance](https://github.com/chipzoller/hugo-clarity#configuration) and update the `www/config.toml` accordingly. I'll document my changes in the [Customization](#Customization) section below.

---

`STEP 5`: Test your website presentation locally

Hugo supports hot reload so you can see the impact of configuration and content changes to your websitee as you make them. The "-D" option indicates draft mode (allowing you to see posts still in draft state) - don't use it if you only want to see published articles.

```
$ cd www/
$ hugo server -D
..
..
Web Server is available at http://localhost:1313/blog/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

---
`STEP 6`: BUILD FOR DEPLOYMENT

The default build directory is local.
Followed this [guidance](https://gohugo.io/getting-started/quick-start/) I updated my `www/config.toml` to specify a custom _publishdir_ ("docs") as the target.

Now just build the static website from this source using this command (again remember that -D will show drafts):

```
$ cd www/
$ hugo -D
```
 
`Note`: Go into the GitHub Settings for gh-pages and point it to the "docs/" folder. You static website is now automatically hosted at the GitHub Pages endpoint for this repo.

---
`STEP 7`: ADD NEW CONTENT TO BLOG

Simply add content into the relevant subfolders using something of the form below, where `xxxxx` is a slug that is unique to the site.

```
$ hugo new posts/xxxxx.md
```

This generates a new file under the `content/posts` directory. If your local server was running, the changes should show up instantly in the browser (hot reload).

---
`STEP 7`:  Automate build/deploy

The current build/deploy process is manual: run the command below (updates `docs/` folder for publication), then commit changes to GitHub to auto-refresh the GHPages static endpoint.

```
$ cd www/
$ hugo -D
```

`TODO:` Automate this step with GitHub Actions.

---

# Customization

 * 



# Troubleshooting

 - Fixed DNS issue (baseUrl update)
 - Fixed side-menu absence (added designer.yml, menu.yml files in data/ folder)
 - Fixed Archives link error (two steps: create new posts in the `content/post` folder, add a `content/_index.md` placeholder)

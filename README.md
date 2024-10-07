# P15
Customized Ghost Source theme
## CSS
- edit files in assets/css
- to build:
```sh
# production
docker exec puntoquindici-ghost-1 /bin/bash -c "cd content/themes/p15Source && yarn pretest"
# staging
docker exec puntoquindici-ghost-1 /bin/bash -c "cd content/themes/p15Source && yarn pretest"
```

## GIT
connect as root with flag -A (pass ssh keys)
```sh
# ssh-add all required keys on local machine
ssh puntoquindici@www.myarstudio.cloud -A
# on www.myarstudio.cloud server
cd /home/puntoquindici/blog/themes/p15Source
git -c user.name="Luca Perusi" -c user.email="luca@puntoquindici.it" commit -m "_MESSAGE_HERE_"
```

## STAGING STRIPES
To immediately recognize the staging website we added stripes in the background of the header.
In ghost we have to patch the admin css.
```sh
docker cp puntoquindici-ghost-dev-1:/var/lib/ghost/versions/5.82.2/core/built/admin/assets/ghost-f84b3f229da06680df6c13ebd46ab671.css ghost-admin.css
cp ghost-admin.css ghost-admin.css.bkp
vim ghost-admin.css
# add css property to 
# .gh-editor-header
# .gh-nav-menu
# background: repeating-linear-gradient(-45deg,rgba(0,0,0,.1),rgba(0,0,0,.1) 15px,rgba(255,235,0,.2) 0,rgba(255,235,0,.2) 30px);
docker cp ghost-admin.css puntoquindici-ghost-dev-1:/var/lib/ghost/versions/5.82.2/core/built/admin/assets/ghost-f84b3f229da06680df6c13ebd46ab671.css
```


------------------------------------------------------------------------------------------------------------------------------



# Source

The default theme for [Ghost](http://github.com/tryghost/ghost/). This is the latest development version of Source! If you're just looking to download the latest release, head over to the [releases](https://github.com/TryGhost/Source/releases) page.

&nbsp;

# First time using a Ghost theme?

Ghost uses a simple templating language called [Handlebars](http://handlebarsjs.com/) for its themes.

This theme has lots of code comments to help explain what's going on just by reading the code. Once you feel comfortable with how everything works, we also have full [theme API documentation](https://ghost.org/docs/themes/) which explains every possible Handlebars helper and template.

**The main files are:**

- `default.hbs` - The parent template file, which includes your global header/footer
- `home.hbs` - The homepage
- `index.hbs` - The main template to generate a list of posts
- `post.hbs` - The template used to render individual posts
- `page.hbs` - Used for individual pages
- `tag.hbs` - Used for tag archives, eg. "all posts tagged with `news`"
- `author.hbs` - Used for author archives, eg. "all posts written by Jamie"

One neat trick is that you can also create custom one-off templates by adding the slug of a page to a template file. For example:

- `page-about.hbs` - Custom template for an `/about/` page
- `tag-news.hbs` - Custom template for `/tag/news/` archive
- `author-ali.hbs` - Custom template for `/author/ali/` archive


# Development

Source styles are compiled using Gulp/PostCSS to polyfill future CSS spec. You'll need [Node](https://nodejs.org/), [Yarn](https://yarnpkg.com/) and [Gulp](https://gulpjs.com) installed globally. After that, from the theme's root directory:

```bash
# install dependencies
yarn install

# run development server
yarn dev
```

Now you can edit `/assets/css/` files, which will be compiled to `/assets/built/` automatically.

The `zip` Gulp task packages the theme files into `dist/<theme-name>.zip`, which you can then upload to your site.

```bash
# create .zip file
yarn zip
```

# PostCSS Features Used

- Autoprefixer - Don't worry about writing browser prefixes of any kind, it's all done automatically with support for the latest 2 major versions of every browser.


# SVG Icons

Source uses inline SVG icons, included via Handlebars partials. You can find all icons inside `/partials/icons`. To use an icon just include the name of the relevant file, eg. To include the SVG icon in `/partials/icons/rss.hbs` - use `{{> "icons/rss"}}`.

You can add your own SVG icons in the same manner.


# Copyright & License

Copyright (c) 2013-2023 Ghost Foundation - Released under the [MIT license](LICENSE).

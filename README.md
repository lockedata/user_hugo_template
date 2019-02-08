# useR website

## What I can do

I can give you most of a website for useR events, ready (almost) out of the box. I have a number of sections to help you out:
* Title Page with:
    + Overview/ About section supporting Markdown
    + Important Dates table
    + Twitter feed section
    + Organising and Programming committee bios
    + Recent News section, supporting markdown blogging
    + Sponsors section
    + Social links in the footer
* Pages supporting Markdown for:
    + Program
    + Participation (ticket registration and paper submission)
    + Venue information (with google maps)
    + News section with all blog posts
    + FAQ
    + Contact section with contact form 
    + Code of Conduct Section
    + About

## What I am
I am a [Hugo](//gohugo.io) website, with two themes. [Universal](https://github.com/devcows/hugo-universal-theme) provides the base layer of theming, with a custom [useR](https://github.com/lockedata/hugo-user-theme/) theme which overides some areas of Universal. The folder `themes/[theme]/layout/partials/` contain all the `.html` needed for the website pages, with the exception of the Markdown, which is saved in `/content/`.

## How to set me up

### Create a new repository
1. Create a new repository on Github for the city & year the site will be for. E.g. https://github.com/[user]/[cityYEAR].git

### Set the repo as a mirror of the main repository
1. Open Git Bash.

2. Create a bare clone of the repository.

  ```
  git clone --bare https://github.com/lockedata/user_hugo_template
  ```

3. Mirror-push to the new repository.

```
cd user_hugo_template.git
git push --mirror https://github.com/[user]/[cityYEAR].git
```

4. Remove the temporary local repository you created in step 1.

```
cd ..
rm -rf user_hugo_template.git
```

### Clone the new repository
1. Now you've removed the temporary local repository, you need to clone the new repository you set up at https://github.com/[user]/[cityYEAR].git

### Initialise the submodules
If you want to run the site locally to view when you're making changes, you need to initialise the submodules
1. Open Git Bash
2. Navigate to the new repo
3. Initialise and fetch the submodules
```
git submodule init
git submodule update
```

### Customise the config
The file [config.toml](https://github.com/lockedata/user_hugo_template/blob/master/config.toml) gives you access to a number of points on the site, mostly using [site params](https://gohugo.io/variables/site/#the-site-params-variable).

A high level overview of these features:
* `enable` 
    + boolean to render or hide that section
* `title`/`subtitle`/`description`/`button text`/...
    + strings to display text in that position
* `bg`
    + boolean to toggle lightly shaded backgrounds on or off for that section
* `photo1`/`photo2`
    + toggle between `background-image-fixed-1`/`background-image-fixed-2` as a background, which are located in `static/img/`
### Bios

The team bios are constructed from the `[[params.programming.members]]` and `[[params.organising.members]]`. Most of these fields are optional and can be deleted to prevent them rendering in the site. 

The icons can be changed per person with [FontAwesome](https://fontawesome.com/).

The headshots are held in `static/img/organising` and `static/img/programming`. The 'faceholder' is in `/themes/hugo-user-theme/static/img/[organising and programming]`, but you should place yours in the root `/static/img/[organising and programming]`, which will mask/override the blanks.

### Sponsors

Sponsor images should be held in `static/img/sponsors`. The files in `/data/sponsors/` control the how and what sponsor image is displayed, and it's location in a folder `tier1`, `tier2`, and `tier3` control where it is on the page.

### Important Dates

Is sourced from a csv stored in `/csv`.

### Content pages

Markdown files are located in `/content`. The News/blog is driven from `/content/blog`, and the other pages in the navbar are driven from the files in `/content/`. An example of how subpages could be constructed is [located in this commit](https://github.com/lockedata/user_hugo_template/commit/211168db3cb975292fd1b8e399669b4c3b24cce0) where the shared 'parent' of 2 `content.md` are specified in the config.

## What if I need even more customistation?
In the hopefully rare event that even more specific material is needed you can explore the following. Make use of the [hugo inheritance method](https://gohugo.io/templates/lookup-order/#hugo-layouts-lookup-rules-with-theme) to override defaults where applicable, rather than modify the defaults in place.

### CSS/style
* Copy the base `hugo-user-theme/static/css/styledefault.css` into `/static/css/style.css` in your root
  + This will now be the style sheet for your website, overriding the themes
  
### New Section/Custom Section
* Either 
  + find a [partial](https://gohugo.io/templates/partials/) from `/layouts/partials` in the existing themes you want to base your work on, copy it to the project `/layouts/partials`, and modify the copy
  + write a new `myfile.html` from scratch and include it in the project `/layouts/partials`
* then make sure that it is referenced in `index.html`

### Deploy to Netlify
1. Set up a "New site from Git" on Netlify using the new repository created in the previous steps
2. Use the build command `hugo`
3. Use the publish directory `public`
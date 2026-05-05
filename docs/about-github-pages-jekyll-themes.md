## What is Github Pages

> It's a way to publish your stuff on the web with near-minimal amounts of effort and configuration.

Github pages:
- allows you to publish webpages at https://[yourName].github.io for free
- can take any branch/directory from your repo and just publish it via https
- is turning your markdown files into html by using Jekyll
- is auto-updating the website every time you push a new change to the repo (on the branch that is chosen as the publishing source)

## What is Jekyll
> It's a static website generator, running on Ruby, taking markdown files in and outputting html structure of a static website (with menus, categories, etc) which can later be published for example via GithubPages

## How can Jekyll driven GithubPages site be customized with jekyll theme?

There are a few ways. We can either:
1. add a name of supported theme repo to the config file
2. add the files of the theme repo to our site repo
3. add the name of supported theme repo to the config file AND some files that are also required to our repo
- Site https://sever.github.io/chirpy-starter
  - Driven by a repo https://github.com/sEver/chirpy-starter

Only the option 1 above gives us relatively clean repo structure with JUST our content. That is not very good.

// TODO: Check if there are differences between adding remote theme via repo url or a Gem?

Suported default github pages themes, available for use with option 1 above:
- https://pages-themes.github.io/architect/
- https://pages-themes.github.io/cayman/
- https://pages-themes.github.io/dinky/
- https://pages-themes.github.io/hacker/ (first with the dark theme)
- https://pages-themes.github.io/leap-day/
- https://pages-themes.github.io/merlot/
- https://pages-themes.github.io/midnight/ (dark)
- https://jekyll.github.io/minima/ (has dark skin)
- https://pages-themes.github.io/minimal/
- https://pages-themes.github.io/modernist/
- https://pages-themes.github.io/slate/
- https://pages-themes.github.io/tactile/
- https://pages-themes.github.io/time-machine/

To be honest, most of them look dated.


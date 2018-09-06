---
title: Excommito theme, blog as you code
description: Excommito is a jekyll theme aimed at developers. Clean layout with nerdy features (dropcaps, post edits history), drafts are made public and can be upvoted to get the author to finish the job.
published: true
link: https://github.com/Kraymer/kraymer.github.io
draft: true
tags:
- jekyll
- open-source
---

*Ex commito* theme is my latest attempt for a minimal theme to empower my blog.

It is based on Hydejack (v5), the pretentious two-column [Jekyll](http://jekyllrb.com) theme derived from [Hyde](http://hyde.getpoole.com).


## Simple and clean layout

- most recent post is featured on homepage
- previous/next post navigation is moved out the post area to the sidebar
- an *article* layout with dropcaps. Code taken from [libretto](https://github.com/ferrolho/jekyll-theme-libretto). Dropcaps can be disabled in the yaml header.
- text is justified
- centered images with optional captions
- unobtrusive social sharing text links in post header section

## A coder theme with unique traits

- introduce a *link* metadata attribute to attach link to a post title. Github logo is appended to article title when the link points to a github project
- solarized dark theme for code excerpts
- *Fingerprint* link in side bar, points to last commit diff
- *History* link in post header, points to current post git history

## Crowdsource the editing process

- *drafts* collection: drafts are published but clearly labeled as 'drafts'. A warning sign in preamble of post content leads to a github issue page where one can vote for the posts drafts he want to see finished. 
- it's shipping reduced to its simple expression : drafts are indexed by google and suggested in the *Kinda related* links section when appropriate. But they do not appear on the Archives section or when using the previous/next post navigation.







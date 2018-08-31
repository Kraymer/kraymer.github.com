---
title: [Django/tests/slack] Unit tests checking translations errors in .po files 
link: https://github.com/Kraymer/django-i18n-police
dropcaps: false
published: true
draft: true
tags:
- python
- django
---

![](/public/img/posts/Selection_055.png)

*Django i18n police* is a set of unit tests detecting human errors in .po files translated strings.  
When tests break it yells on your slack dev channel complaining that a translation ...
- ... is missing
- ... is a url and contains non ASCII characters
- ... contains forbidden characters (eg `%` that is interpreted as a formatting character)
- ... is an url having a different structure than source url
- ... placeholders names don't match those in source string 
- ... markups are unbalanced

You can configure your poeditor API key to have stats about projects completions and links pointing to 
translations to edit in case of errors.

`TODO`: open source the code

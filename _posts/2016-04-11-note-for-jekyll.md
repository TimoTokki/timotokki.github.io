---
layout: post
tag:
    - jekyll
    - study notes
---

_config.yml


For technical reasons, this file is *NOT* reloaded automatically when you use 'jekyll serve'. If you change this file, please restart the server process.

<time></time>>

是H5新标签，但未得到广泛应用

{{ post.content | strip_html | truncatewords:20}}

 | strip_html 是过滤器，过滤掉html标签;| truncatewords:20也是过滤器，限制字数
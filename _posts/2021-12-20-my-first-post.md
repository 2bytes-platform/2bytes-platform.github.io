---
layout: post
title: "๐ github pages๋ฅผ ์ด์ฉํ ์ ์  ์น์ฌ์ดํธ ๊ตฌ์ฑํ๊ธฐ"
excerpt: "github pages ์ด์ฉํ์ฌ ์น์ฌ์ดํธ ๊ตฌ์ฑํด๋ณด์"
subtitle: ""
toc: true
toc_sticky: true
toc_label: "ํ์ด์ง ์ฃผ์ ๋ชฉ์ฐจ"
date: 2021-12-20
tags: [github_pages]
---

## guthub blog๋ฅผ ์์ฑํ๋ ๊ณผ์ ์ ๋ํด์ ์์ ํ๊ฒ ์.  
ํด๋น ๋ธ๋ก๊ทธ๋ฅผ ์ฐธ์กฐํ์ฌ github pages๋ฅผ ๊ตฌ์ฑํ์์  
[GitHub Pages ๋ธ๋ก๊ทธ ์๊ฐ](https://devinlife.com/howto%20github%20pages/github-blog-intro/)

Jekyll์ ๋ฃจ๋น๋ก ๋ง๋  ์ ์  ์น์ฌ์ดํธ ์์ฑ๊ธฐ์ด๋ฉฐ, md๋ก ์์ฑ๋ ์ปจํ์ธ ๋ฅผ html๋ก ๋ณํํด์ฃผ๋ ์ญํ ์ ๊ฐ๊ณ  ์์.

๋ค์๊ณผ ๊ฐ์ ์์ผ๋ก ํฌ์คํ์ ์์ํ์

1. md๋ก ์ปจํ์ธ ๋ฅผ ์์ฑํ๋ค  
2. ๋ก์ปฌ์์ bundle exec jekyll serve๋ฅผ ์คํํ์ฌ, ๊ฒ์  
3. ๊ฒ์ ํ, ์ฐ๊ฒฐ๋ remote repo๋ก commit & push ํ๋ฉด ๋  


## ๋ค์๊ณผ ๊ฐ์ ์์ผ๋ก ํ๊ฒฝ์ ๊ตฌ์ถํ์

- ruby ์ค์น  
- Jekyll๊ณผ bundler ์ค์น  
  - ์ต์ ๋ฒ์ ์ผ๋ก ์์ฑํ์  
  - 'jekyll new HelloBlog'๋ก ์ํ ๋ธ๋ก๊ทธ๋ฅผ ์์ฑ
  - 'bundle exec jekyll serve'
- minimal-mistakes theme ์ธํ, [<mmistakes repo></mmistakes>](https://github.com/mmistakes/minimal-mistakes)์์ ๋ก์ปฌ๋ก clone ํ, ํ์์๋ ํ์ผ์ ์ญ์   
  bundle ๋ช๋ น์ด๋ฅผ ์คํํ์ฌ ํ์ํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ๋ค ์ค์นํด์ฃผ์ [<mmistakes guide></mmistakes>](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)  
  gem minimal-mistakes-jekyll๋ก ์ค์น 
- username.github.io๋ก repo ์์ฑ ํ, public ์ค์ 
- remote repo์ local repo๋ฅผ ์ฐ๊ฒฐํ์

- [`require': cannot load such file -- webrick (LoadError)](https://junho85.pe.kr/1850)
- git ์ค์นํด์ bash ์ปค๋งจ๋์ฐฝ ์ด์ฉ 
- ๊ฒ์ ๊ธฐ๋ฅ ์ง์ํ๋์ง ์ฐพ์๋ณด์ 
- minimal mistakes Gemfile ๊ด๋ จ ์ค๋ฅ ๋ฐ์ ์, ์ง์  ๋ณต๋ถํด์ ๋ถ์ฌ๋ฃ์
  ```ruby
  source "https://rubygems.org"

  # Hello! This is where you manage which Jekyll version is used to run.
  # When you want to use a different version, change it below, save the
  # file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
  #
  #     bundle exec jekyll serve
  #
  # This will help ensure the proper Jekyll version is running.
  # Happy Jekylling!

  # gem "github-pages", group: :jekyll_plugins

  # To upgrade, run `bundle update`.

  gem "jekyll"
  gem "minimal-mistakes-jekyll"

  # The following plugins are automatically loaded by the theme-gem:
  #   gem "jekyll-paginate"
  #   gem "jekyll-sitemap"
  #   gem "jekyll-gist"
  #   gem "jekyll-feed"
  #   gem "jekyll-include-cache"
  #
  # If you have any other plugins, put them here!
  # Cf. https://jekyllrb.com/docs/plugins/installation/
  group :jekyll_plugins do
  end
  gem "webrick", "~> 1.7"
  ```
trouble shooting: [mmistakes Installation](https://mmistakes.github.io/minimal-mistakes/docs/installation/)
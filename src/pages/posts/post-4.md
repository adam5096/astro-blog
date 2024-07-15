---
layout: ../../layouts/MarkdownPostLayout.astro
title: '我的第4篇文章'
author: 'Astro 學習者'
description: "這篇文章會自己出現在列表中！"
image:
  url: "https://docs.astro.build/default-og-image.png"
  alt: "The word astro against an illustration of planets and stars."
pubDate: 2022-08-08
tags: ["astro", "successes"]
---
這篇文章應該會與其他的部落格文章一起顯示，因为 `Astro.glob()` 會返回一个包含所有文章的列表，以建立這個文章列表。
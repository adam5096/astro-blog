---
title: "我的第2篇文章"
pubDate: 2024-07-11
description: "這是我的部落格中第2篇文章."
image:
  url: "https://docs.astro.build/default-og-image.png"
  alt: "The word astro against an illustration of planets and stars."
author: "Adam"
tags: ["astro", "freeze", "once", "text", "html"]
---

# Day 2：實體化與模板語法
點我看更多👉[https://www.youtube.com/live/52Uu1VhsYI8?si=Gb8o5l8CdigeoisU](https://www.youtube.com/live/52Uu1VhsYI8?si=Gb8o5l8CdigeoisU)

0:41:44
**如何從畫面/設計稿去推論出合理的數據結構規劃**

```jsx
const pokemon={
    img:string,
    img:{
         src:'str',
         alt:'str/html'
        },
    title:'str/html',
    desc:'str/html',
    price:'number',
    price:{
          type:'str',
          count:'number'
    },
    count:'number'
}
```

0:44:29  
todomvc[https://todomvc.com/](https://todomvc.com/)

0:46:48  
```Object.freeze(data)```

效能議題  
淺層為時間管理  
深層為空間管理(記憶體)

0:59:58  
請問方法前方帶金錢符號```$```是甚麼意思  
為了把vue自帶的私有功能，與工程師自做的功能區分開來，私有功能通常帶$符號

1:29:25  
v-once

1:35:16  
合併內容 或 取代內容?  
```{{ }}```
v-text  
v-html

1:54:51  
**javascript 表達式**  
在template結構僅允許渲染白名單上全域變數, 名單見官網  
[https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9)

2:10:18  
**vue 生命週期理解  Option API寫法**  
el, template兩者的存在與否, 對渲染頁面有哪些影響, 可舉例說明

instance $ template
1. html template + el option
2. el option + template option
3. template option + vm$mount
---
title: "我的第1篇文章"
pubDate: 2024-07-11
description: "這是我的部落格中第1篇文章."
image:
  url: "https://docs.astro.build/default-og-image.png"
  alt: "The word astro against an illustration of planets and stars."
author: "Adam"
tags: [ "astro", "cloak", "api", "Date", "getFullYear", "json" ]
---

# [ 想入門，我陪你 ] Re Vue 重頭說起 Day 1：基本介紹與起步安裝
點我看更多👉[https://www.youtube.com/live/Y50_RSWpWkA?si=DwKlps1IQYux0VLz](https://www.youtube.com/live/Y50_RSWpWkA?si=DwKlps1IQYux0VLz)

1:45:07  
**VUE樣板語法和純HTML有哪些不同**  
滑鼠點右鍵 => 檢視網頁來源

2:01:08  
year: '@' + new Date().getFullYear()

**2:07:17**  
**使用前端框架一定要配API嗎?**  
資料的來源
1. 資料寫在程式碼裡
2. 資料與主程式拆分, 資料獨立寫成 JSON 檔, 搭配AJAX, 搭配 JSON server(靜態API)
3. 有來自 server 的 API(真-API)

**2:19:18**  
請問有時候因為網速問題, js(vue)執行太慢, 未經vue渲染直接把語法印在頁面上, 我們不希望讓使用者看到這些, 可以如何優化這件事?
1. v-cloak工作原理  
未啟動 vue 時, v-cloak包裹範圍, 其內容不會出現在頁面上(配合css設定display:none)
當 vue 啟動並解析到v-cloak語法時, 會將v-cloak拔掉, 展示經vue完整渲染後的頁面
2. v-cloak使用時機  
[cloak] {
    display:none
}

**2:29:44**  
Promise  
async await
```jsx
// await 循序處理
// 瀏覽器拿到資料往data1裡面存好後, 才接著往下做data2, data3 
let data1 = await axios.get(...)
let data2 = await axios.get(...)
let data3 = await axios.get(...)

Promise.all([data1,data2,data3]).then(function(){
    // 全部都對, 就走這裡
}).catch(function(){
    // data1,data2,data3 不分順序, 任何一個出錯, 走這裡
})
```
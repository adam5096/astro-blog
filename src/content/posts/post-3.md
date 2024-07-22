---
title: "我的第3篇文章"
pubDate: 2024-07-11
description: "這是我的部落格中第3篇文章."
image:
  url: "https://docs.astro.build/default-og-image.png"
  alt: "The word astro against an illustration of planets and stars."
author: "Adam"
tags: [ "astro", "computed", "split", "reverse", "join", "methods", "caching", "watch" ]
---

# Day 3：資料計算與偵聽
點我看更多參考資料👉[https://www.youtube.com/watch?v=3wvoDxZq52w&list=PLEfh-m_KG4dapPjoPvWX0c8JCK6-mIvGr&index=4](https://www.youtube.com/watch?v=3wvoDxZq52w&list=PLEfh-m_KG4dapPjoPvWX0c8JCK6-mIvGr&index=4)

0:14:41  
**computed**  
翻過來  
建議使用場景：當需要使用原始資料來產生其他衍伸資料時

0:23:58
option api寫法中
**data** option 屬性名稱和 **computed** option屬性名稱, 兩者重名, 可能有甚麼影響?會報錯嗎?  
1. 沒有影響
2. 有影響, 影響是console報錯: the computed property "message" is already defined in data

```jsx
<div id="#app">
    {{ message }}
</div>

<script></script>
new Vue({
    el:'#app',
    data: {
        message:'Hello'
        },
    computed: function(){
        return this.message.split('').reverse().join('')
    }
})
```

```jsx
<div id="#app">
    {{ reversedMessage }}
</div>

<script></script>

new Vue({
    el:'#app',
    data: {
        message:'Hello'
        },
    computed: {
        reversedMessage: function(){
        return this.message.split('').reverse().join('')
        }
    }
})
```

0:36:37  
**為什麼要使用computed**
1. 從用法上, 表達上, 傾向優先選用computed
    - computed 被看作屬性
    - **操作**上就同讀取變數一樣
    - **辨別、認知、解讀**上這是一筆資料、變數、參數

    methods 被看作函數
    - **操作**他就同操作函數一樣去呼叫
    - **辨別、認知、解讀**上這是函數
    - 函數的執行結果可以是return資料、執行內容、執行功能

```jsx
<div id="#app">
    computed: {{ reversedMessage }}
    methods: {{ reversedMessage() }}
</div>

<script></script>

new Vue({
    el:'#app',
    data: {
        message:'Hello'
        },
    computed: {
        reversedMessage: function(){
        return this.message.split('').reverse().join('')
        }
    },
    methods: {
        reversedMessage1: function(){
        return this.message.split('').reverse().join('')
        }
    },
})
```

0:44:31  
**computed caching**

```jsx
<div id="#app">
    computed: {{ reversedMessage }}
    methods: {{ reversedMessage() }}
</div>

<script></script>

new Vue({
    el:'#app',
    data: {
        message:'Hello'
        },
    computed: {
        reversedMessage: function(){
        console.log('computed')
        return this.message.split('').reverse().join('')
        }
    },
    methods: {
        reversedMessage1: function(){
        console.log('methods')
        return this.message.split('').reverse().join('')
        }
    },
})
```

1:06:31  
是否在template存取/展示/使用某筆data  
=> DOM是否更新  
=> 畫面是否更新

如果computed計算過後的衍生資料要能夠引起畫面重新渲染  
通常computed的**資料來源**包括(但不限於)是來自  
1. data option  中的屬性與值
2. store(vuex和pinia中倉庫資料)
3. 甚至來自二手三手之後的其他computed

1:20:44  
**watch  作者分享使用案例**
1. 來源數據變化=>
2. 經過發起API請求到server校驗資料並接收回傳數據=>
3. 接收數據並與瀏覽器本地數據比對發現不同後，可考慮用watch監聽來源數據變化

如來源數據只是簡單變化(數據變化前、後所經的流程較簡單、單純)  
如+-*/, 合併?則先選computed即可

接上文, 請用vue3, quasar2幫我打造一個企業形象官方網站
包含以下要求
1. 用quasar-cli做構造工具
2. 說明並展示src目錄結構與安排
3. 簡單使用pinia與vue-router
4. 簡單使用RESTful API
5. 為每個段落的程式碼做說明與註解
謝謝

OWASP TOP 10
1. **A01:2021-Broken Access Control** moves up from the fifth position to the category with the most serious web application security risk; the contributed data indicates that on average, 3.81% of applications tested had one or more Common Weakness Enumerations (CWEs) with more than 318k occurrences of CWEs in this risk category. The 34 CWEs mapped to Broken Access Control had more occurrences in applications than any other category.
2. **A02:2021-Cryptographic Failures** shifts up one position to #2, previously known as A3:2017-Sensitive Data Exposure, which was broad symptom rather than a root cause. The renewed name focuses on failures related to cryptography as it has been implicitly before. This category often leads to sensitive data exposure or system compromise.
3. **A03:2021-Injection** slides down to the third position. 94% of the applications were tested for some form of injection with a max incidence rate of 19%, an average incidence rate of 3.37%, and the 33 CWEs mapped into this category have the second most occurrences in applications with 274k occurrences. Cross-site Scripting is now part of this category in this edition.
4. **A04:2021-Insecure Design** is a new category for 2021, with a focus on risks related to design flaws. If we genuinely want to "move left" as an industry, we need more threat modeling, secure design patterns and principles, and reference architectures. An insecure design cannot be fixed by a perfect implementation as by definition, needed security controls were never created to defend against specific attacks.
5. **A05:2021-Security Misconfiguration** moves up from #6 in the previous edition; 90% of applications were tested for some form of misconfiguration, with an average incidence rate of 4.5%, and over 208k occurrences of CWEs mapped to this risk category. With more shifts into highly configurable software, it's not surprising to see this category move up. The former category for A4:2017-XML External Entities (XXE) is now part of this risk category.
6. **A06:2021-Vulnerable and Outdated Components** was previously titled Using Components with Known Vulnerabilities and is #2 in the Top 10 community survey, but also had enough data to make the Top 10 via data analysis. This category moves up from #9 in 2017 and is a known issue that we struggle to test and assess risk. It is the only category not to have any Common Vulnerability and Exposures (CVEs) mapped to the included CWEs, so a default exploit and impact weights of 5.0 are factored into their scores.
7. **A07:2021-Identification and Authentication Failures** was previously Broken Authentication and is sliding down from the second position, and now includes CWEs that are more related to identification failures. This category is still an integral part of the Top 10, but the increased availability of standardized frameworks seems to be helping.
8. **A08:2021-Software and Data Integrity Failures** is a new category for 2021, focusing on making assumptions related to software updates, critical data, and CI/CD pipelines without verifying integrity. One of the highest weighted impacts from Common Vulnerability and Exposures/Common Vulnerability Scoring System (CVE/CVSS) data mapped to the 10 CWEs in this category. A8:2017-Insecure Deserialization is now a part of this larger category.
9. **A09:2021-Security Logging and Monitoring Failures** was previously A10:2017-Insufficient Logging & Monitoring and is added from the Top 10 community survey (#3), moving up from #10 previously. This category is expanded to include more types of failures, is challenging to test for, and isn't well represented in the CVE/CVSS data. However, failures in this category can directly impact visibility, incident alerting, and forensics.
10. **A10:2021-Server-Side Request Forgery** is added from the Top 10 community survey (#1). The data shows a relatively low incidence rate with above average testing coverage, along with above-average ratings for Exploit and Impact potential. This category represents the scenario where the security community members are telling us this is important, even though it's not illustrated in the data at this time.

回想自己第1、2位補教機構老師們，他們替學生先消化完文件後，設計好教材內容，
從npm create vue 邊爬邊扶一路陪著到npm run build
殘酷的是努力回想，發現已經忘記接近一半的開發流程
(第一個專案花去我2個多月時間, 我另外盤點老師的開發時間，老師才花約40小時出頭)
這好像去駕訓班學開車，會漸漸熟悉駕訓班的教練車與道路，待真實上路又是另一套環境
.
ALEX大頻道是我在網路上茫茫學習資源遇到的第一位帶看文檔的前輩(我就定下來不隨波逐流了XD)
自己埋頭啃文件，常常是雲裡霧裡走到迷路，學習路上有明燈和指南針最幸福
期待ALEX大大頻道未來的新內容(包含幹話台哈哈哈)
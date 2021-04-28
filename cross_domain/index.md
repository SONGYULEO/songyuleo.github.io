# [C#、JQuery]Cross-Domain server 端處理

紀錄一下許早之前遇到的`Cross-Domain`問題，在Local測試得很開心都沒問題，一把東西丟到測試環境這問題就出現了...
<!--more-->

原因可以參考WIKI的介紹[`Cross-origin resource sharing`](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)

簡單來說用Ajax向非同域請求資源會先丟一個`預檢(preflight)` HTTP OPTIONS 的方法給Server端檢驗，若通過才會丟正式的request出去(get、post等等)，若非允許的`跨域`請求的需求沒有處理會被Reject，造成Ajax失敗，解法有很多種，但我還是用最簡單的方式`Access-Control-Allow-Origin`針對server端處理。

## 1. 解說
#### web.config內的<system.webServer>加入紅框部分，`*`代表允許任何人存取
![](https://i.imgur.com/FSsguRv.png)



> 注意:這樣的方式很快但不代表適合任何人，若要限制也可以這樣寫`Access-Control-Allow-Origin: http://xxxxx.com`

#### 其他也有`JsonP`的方式也是不錯的方式，有機會再發表一篇來解說吧~



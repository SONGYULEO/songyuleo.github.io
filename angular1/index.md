# [AngularJS] $broadcast , $emit , $on 事件處理機制筆記


公司專案使用[`AngularJs 1.6`](https://code.angularjs.org/1.6.10/docs/guide/migration)開發,面對使用者複雜又特殊的requirement ，一個page切多個`controller`也方便未來維護，那`controller`間如何來互相傳值呢?

<!--more-->

在`AngularJs`中 `$emit` , `$broadcast` and `$on` 用來處理各`controller`事件處理






- [`$on`](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$on)用來接收`$emit` , `$broadcast`的事件(event)

- [`$emit`](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$emit)能向父級別parent controller傳遞事件(event)與資料(data)

- [`$broadcast`](https://docs.angularjs.org/api/ng/type/$rootScope.Scope#$broadcast)向子級別child controller傳遞事件(event)與資料(data)





## 1. 說明
- 若同父級別向子級別傳遞事件(`$broadcast`)，多個同`level`子級別的`controller` 可以一起接收到事件,但其中一個子級別傳遞事件(`$emit`)，只有這個子級別的父級別可以收到事件，其他同`level`父級別`controller`無法收到事件

### 1. Example


<iframe height='465' scrolling='no' title='AngularJs $emit , $broadcast and $on Example Note' src='//codepen.io/SungYuHe/embed/eKjpzb/?height=265&theme-id=dark&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/SungYuHe/pen/eKjpzb/'>AngularJs $emit , $broadcast and $on Example Note</a> by LeoHe (<a href='https://codepen.io/SungYuHe'>@SungYuHe</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>




### 2. 參考
[AngularJs function](https://docs.angularjs.org/api/ng/function)

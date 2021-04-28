# [C#]自訂排序(Custom Sort)

User這次給了一道題目，按照指定的規則且多個條件下排序資料...，這非得要實作[`IComparable`](https://msdn.microsoft.com/zh-tw/library/system.icomparable&#40;v=vs.110&#41;.aspx)來實現了。 
<!--more-->

在範例中有以下幾個重點

- 第一次排序為指定順序(`Space`冒號前的字串先排序)

- 第二次排序為小到大排序(`Space`整個排序)

- 第三次排序為小到大排序(`Item`排序)


## 1. Example

<iframe height="600px" width="100%" src="https://repl.it/@sungyuhe/Zi-Ding-Pai-Xu-Custom-Sort?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

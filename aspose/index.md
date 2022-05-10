# [C#]Aspose for . NET 筆記

呼 已經許久沒更新文章了，距離上一次是2018...，當然這之中也經歷了職涯轉換、部落格由原本的Hexo 換到Hugo 等，再來陸陸續續會慢慢整理弄上來。

---

相信在公司碰過文件轉換的需求（如word to pdf），特別又是office 系列一定用過***DCOM***來處理這個問題，但微軟已經不support 這個元件，所以使用上只能祈禱不會遇到問題。。（偏偏就是遇到問題了這篇才生出來的
<!--more-->
所以就開始Survey 一些不靠DCOM也能轉的套件，找了幾間最後還是看上    Aspose ，聯絡了一下拿到了 Temporary License 

但原先提供的simple code 看似兩三行可以解決，純英文的文件或許可行，但遇到其他語言如高綿文就會發現轉出來的PDF還是會有亂碼。。。
```
Aspose.Words.License lic = new Aspose.Words.License();

lic.SetLicense(path + "Aspose.Words.lic");

Document doc = new Document(path + "input.docx");

doc.Save(path + "output.pdf");
```

後來得知需要 ***Enable OpenType Features*** 才行～

## 1. Nuget 安裝


要先從Nuget安裝以下兩個套件

![image-20210430161440048](/images/posts/image-20210430161440048.png)

- Aspose.Words
- Aspose.Words.Shaping.HarfBuzz

## 2. 範例
(ps.範例為原始word轉pdf)
```
MemoryStream ms = new MemoryStream();

uploadfile.CopyTo(ms);

Document doc = new Document(ms);

var path = @"./file/" + uploadfile.FileName".pdf";

doc.LayoutOptions.TextShaperFactory = Aspose.Words.Shaping.HarfBuzz.HarfBuzzTextShaperFactory.Instance;

doc.Save(path);
```




# [C#]切換不同環境 Entity 

在開發期間使用的Entity是在test環境下，但要切換到正式環境不用整個專案review一次或者把entity拿掉才能切換過去，不能針對xxx.edmx底下的`DbContext`直接修改，這是系統自動產生的，但可以再另外partail class要切換的Connection name 。
<!--more-->
ps.這邊是系統自動產生，不要在這邊修改
![](https://i.imgur.com/47ZiRig.png)


----------


## 1. 解說

### 1.1 在專案中產生一個Partial class 

```
    public partial class Entities : DbContext
    {
        public Entities (string ConnectionString):base(ConnectionString)
        {


        }
        
    }
    public class SwitchDbContext
    {
        public Entities CreateDbContext(string connectionstring)
        {
            switch (connectionstring)
            {
                //QA連線
                case "QA":
                    return new Entities();

                //Production連線
                case "Production":
                    return new Entities("name=EntitiesP");

                //預設為QA連線
                default:
                    return new Entities();
            }
        }
    }
```
<br />
### 1.2 修改設定檔

#### 接下來到`app.config` or `web.config` 裡面找到`<appSettings>`加入這些，這樣未來只要改`app.config` or `web.config`就能切換。
![](https://i.imgur.com/45R8XsN.png)

<br />
##### 一樣到`app.config` or `web.config` 裡面找到`<connectionStrings>`後複製`name=Entities`這一條，在下方貼上並將`name`改成`EntitiesP`，`ConnectionString`需自行修改成自己的正式環境資訊。
![](https://i.imgur.com/tFJGhht.png)

<br />

##### 接下來在原先宣告Entity的地方改成如下圖,如需切換Entity Connection只要修改`app.config` or `web.config`<appSettings>裡面的內容就好了。
![](https://i.imgur.com/d8A6O3V.png)




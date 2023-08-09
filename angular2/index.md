# [Angular]使用HttpInterceptor 處理HttpRequest和HttpResponse


通常前端專案很常使用[HttpClient](https://angular.io/api/common/http/HttpClient)來與後端API互動，而如果需要Token認證或需要在每次的請求處理一些log機制等就需要在每一次實作HttpClient都撰寫相似的程式碼....

<!--more-->

<br>

自從 Angular 4.3 開始新增了[HttpInterceptor](https://angular.io/api/common/http/HttpInterceptor) 攔截器，可以處理每次的請求與回應間須"加工"的過程，其類似ASP.NET Core中的Middleware


![Alt text](imgs/image-1.png)


<br>

接下來為如何實作HttpInterceptor攔截器 (範例為 Angular 13)



## 1. 新增interceptor service

### 1.1 在專案內新增一個 HTTPInterceptor.ts service ，並參考下方範例


```typescript
import { Injectable } from '@angular/core';
import {
  HttpEvent, HttpInterceptor, HttpHandler, HttpRequest
} from '@angular/common/http';

import { Observable } from 'rxjs';

@Injectable()
export class HTTPInterceptor implements HttpInterceptor {

  intercept(req: HttpRequest<any>, next: HttpHandler):
    Observable<HttpEvent<any>> {

    //在發出request前要處理的部分

    return next.handle(req);
  }
}

```


### 1.2 到app.module.ts 註冊HTTPInterceptor 攔截器
```typescript
@NgModule({
  bootstrap: [AppComponent],
  imports: [...],
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: HTTPInterceptor,
      multi: true
    }
  ]
})
export class AppModule {}
```

<br>

<h3>過來看看進階用法</h3>

<br>


## 2.  interceptor service 進階

### 2.1 request header

這邊示範當拿到token(最常見為登入所取得的JWT)，來當每一次request 的認證

```typescript
import { Injectable } from '@angular/core';
import {
  HttpEvent, HttpInterceptor, HttpHandler, HttpRequest
} from '@angular/common/http';

import { Observable } from 'rxjs';

@Injectable()
export class HTTPInterceptor implements HttpInterceptor {

  intercept(req: HttpRequest<any>, next: HttpHandler):
    Observable<HttpEvent<any>> {

    //在每一次request 均加入Authorization header
    req = req.clone({
       setHeaders: {
          Authorization: `Bearer ${token}`,
        },
      })

    return next.handle(req);
  }
}

```

### 2.2 error handle 

這邊會用到rxjs 相關的應用(observable & operators)



```typescript
import { Injectable } from '@angular/core';
import {
  HttpEvent, HttpInterceptor, HttpHandler, HttpRequest
} from '@angular/common/http';

import { Observable } from 'rxjs';

@Injectable()
export class HTTPInterceptor implements HttpInterceptor {

  intercept(req: HttpRequest<any>, next: HttpHandler):
    Observable<HttpEvent<any>> {

    const retryCount = 3;
    const retryWaitMilliSeconds = 1000;

    return next.handle(req).pipe(
        //當response 為特定code 作相應處理
        catchError((err: HttpErrorResponse) => {
            switch (err.status) {
              case 400:
                
                //400 code handle

                break;
              case 401:

                //401 code handle

                break;
              case 404:

                //404 code handle

                break;

              default:

                break;
            }
          return EMPTY;
        }),
        //retry 3次、間隔1000毫秒
        retry({ count: retryCount, delay: retryWaitMilliSeconds })
        );
  }
}

```



---
## 參考
[Angular HTTP Interceptor](https://angular.io/guide/http-intercept-requests-and-responses)

[Rxjs retry](https://www.learnrxjs.io/learn-rxjs/operators/error_handling/retry)

[Rxjs catchError](https://www.learnrxjs.io/learn-rxjs/operators/error_handling/catch)




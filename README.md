# ComputerScience
기초 컴퓨터 사이언스 지식에 대해 기록합니다.





## HTTP 개요

웹에서 이루어 지는 모든 데이터 교환에 사용되는 프로토콜 

클라이언트-서버 프로토콜 이라고도 합니다.  TCP/IP 프로토콜 기반으로 만들어진 프로토콜 입니다.

어플리케이션 레벨의 프로토콜로써, HTTP 프로토콜에서 사용하는 내용을 <u>'메시지'</u> 라고 부릅니다. 



![image-20211021163747358](C:\Users\sukang\AppData\Roaming\Typora\typora-user-images\image-20211021163747358.png)

클라이언트에서 요청되는것을 보통 **HTTP Request** 라 하고, 서버에서의 응답을 **HTTP Response** 라고 정의 합니다. 



### HTTP Headers

### 

#### 공통 헤더

- **Content-Type** : 해당 요청/응답에 포함되는 미디어 타입 정보 컨텐츠의 타입 및 문자 인코딩 방식을 지정

- **Content-Encoding** : 해당 개체 데이터의 압축 방식 

- **Content-Length** : 전달되는 해당 개체의 바이트 길이 또는 크기 (10진수)

  

#### 요청 헤더

- **Host** : 요청하는 호스트에 대한 호스트 명 및 포트번호 (필수)
- **User-Agent** : 클라이언트 소프트웨어 명칭 및 버전 정보 
- **Cookie** : 서버에 의해 Set-Cookie로 클라이언트에게 설정된 쿠키 정보 
- **Authorization** : 인증 토큰을 서버로 보낼 때 사용하는 헤더 
- **Accept** : 클라이언트 자신이 원하는 미디어 타입 및 우선 순위를 알린다. 
- **Accept-Language** : 클라이언트 자신이 원하는 가능한 언어 
- **Accept-Encoding** : 클라이언트 자신이 원하는 문자 인코딩 방식



### 요청 예시 

```http
GET /home.html HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/ *;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/testpage.html
Connection: keep-alive
Upgrade-Insecure-Requests: 1
If-Modified-Since: Mon, 18 Jul 2016 02:36:04 GMT
If-None-Match: "c561c68d0ba92bbeb8b0fff2a9199f722e3a621a"
Cache-Control: max-age=0
https://gmlwjd9405.github.io/2019/01/28/http-header-types.html
```



참조 블로그 주소 : https://gmlwjd9405.github.io/2019/01/28/http-header-types.html



### HTTP Status Code 



### HTTPS



### HTTP 구조



### HTTP Developement Tool



### CORS (Cross-Origin Resource Sharing) 교차 출처 리소스 공유 : 

웹어플리케이션은 리소스가 자신의 출처 (도메인, 프로토콜, 포트) 와 다를 때 교차 출처 HTTP 요청을 실행 합니다. 

보안 상의 이유로 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청을 제한 합니다. 원칙적으로 웹어플리케이션은 자신과 동일한 출처의 리소스만 불러올 수 있으며, 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환 해야 합니다. 

CORS 문제는 브라우저 에서, Javascript XMLHttpRequest 와 Fetch API 호출 시 해당 CORS 문제 발생 가능 

![image-20211021185421217](C:\Users\sukang\AppData\Roaming\Typora\typora-user-images\image-20211021185421217.png)



CORS 문제가 발생 하게 되면, API 서버 로직에서 이를 처리해 주어야 합니다. 언어별로 처리해주는 방법은 각각 다르나, C# (ASP.NET Core / ASP.NET ) 에서는 아래와 같이 지원할 수 있습니다. 



**Case : ASP.NET Core 에서 CORS 지원 하기.** 

```c#
          
/* ASP.NET Core Startup.cs 에 다음 내용 추가*/
services.AddCors(options =>
            {
                options.AddPolicy("CORS Configuration", builder =>
                {
                    builder.AllowCredentials() 
                           .AllowAnyHeader() // 어떤 HTTP Header 도 허용한다. 
                           .AllowAnyMethod(); // 어떤 HTTP Method 도 허용한다. 
                });
            });

```

**Case : ASP.NET 에서, CORS 지원 하기** 

관련 링크 : https://docs.microsoft.com/ko-kr/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api 

```c#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```



**Case : Controller 로직에서 지원하기**

```c#
[EnableCors(origins: "http://www.example.com", headers: "*", methods: "get,post")]
public class TestController : ApiController
{
    public HttpResponseMessage Get() { ... }
    public HttpResponseMessage Post() { ... }
    public HttpResponseMessage Put() { ... }    
}

[EnableCors(origins: "*", headers: "*", methods: "*", exposedHeaders: "X-Custom-Header")]
public class TestController : ApiController
{
    public HttpResponseMessage Get()
    {
        var resp = new HttpResponseMessage()
        {
            Content = new StringContent("GET: Test message")
        };
        resp.Headers.Add("X-Custom-Header", "hello");
        return resp;
    }
}
```







## RESTful



## HTTPS HandShake



## WAS vs WebServer



## Cookie 



## Session 



## Local Storage / Session Storage 



## CORS



## 브라우저 렌더링 과정








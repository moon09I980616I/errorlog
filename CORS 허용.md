# CORS

출처 : 

[https://velog.io/@ohzzi/CORS-허용-좀-해주세요](https://velog.io/@ohzzi/CORS-%ED%97%88%EC%9A%A9-%EC%A2%80-%ED%95%B4%EC%A3%BC%EC%84%B8%EC%9A%94)

https://bohyeon-n.github.io/deploy/web/cors.html 

: (CrossOrigin annotation 코드에서 parameter origin → origins)

# CORS;Cross-Origin Resource Sharing

교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)는 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제입니다. 웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행합니다.

쉽게 설명하자면 CORS란 도메인이 다른 서버끼리 리소스를 주고 받는 정책이라고 생각하면 됩니다. 이게 왜 문제가 되냐면, 기본적으로 웹 브라우저의 기본 정책은 `Same-Origin`으로, `origin`이 다른 서버와의 리소스 공유를 허용하고 있지 않기 때문입니다.

여기서 `origin`이란 `scheme(일반적으로 프로토콜)`, `host(도메인)`, `port`를 모두 포함하는 것으로, 셋 중 하나라도 일치하지 않는다면 다른 `origin`으로 판단합니다. 예를 들어, 한 컴퓨터에서 React 서버(3000 포트)와 Springboot(8080 포트) 서버를 모두 띄워서 서로 리소스를 주고 받으려 한다면 포트가 다르기 때문에 `origin`이 달라 CORS 위반 문제가 발생하고, 개발자 도구 창에서는 시뻘건 CORS 위반 에러 메시지를 볼 수 있게 됩니다.

그래서 서버에서는 "어? 요청이 왔네?" 하고 200번대 OK 상태 코드를 응답하고 리소스를 정상적으로 보내더라도, 응답을 받은 뒤 브라우저가 판단하기에 "아 이거 같은 `origin`이 아니네."하고 판단해서 에러를 띄워버립니다. 결론적으로, 서버에서는 CORS 위반을 확인할 수 없습니다.

### **CORS는 어떻게 작동하는가?**

**Preflight Request**

기본적으로 브라우저는 HTTP 요청을 보낼 때, 사전에 `OPTIONS` 메서드를 통한 HTTP 요청을 보내서 요청을 보내기 안전한지 확인해야 합니다. 미리 전송(preflight) 한다고 해서 이를 `프리플라이트 요청(preflight request)`이라고 하는데요, 이 때 요청하려는 메서드 정보를 `Access-Control-Request-Method` 헤더에, 요청에 담길 헤더 정보를 `Access-Control-Request-Headers` 헤더에 담습니다.

```jsx
OPTIONS /resources/post-here/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Connection: keep-alive
Origin: http://foo.example
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-PINGOTHER, Content-Type
```

이런 식으로. 그러면 서버는 응답으로 어떤 것을 허용하는지에 대한 정보를 담아서 돌려줍니다.

```jsx
HTTP/1.1 204 No Content
Date: Mon, 01 Dec 2008 01:15:39 GMT
Server: Apache/2
Access-Control-Allow-Origin: https://foo.example
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: X-PINGOTHER, Content-Type
Access-Control-Max-Age: 86400
Vary: Accept-Encoding, Origin
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
```

이런 식으로 `Access-Control-Allow-Origin`에는 허용된 `origin` 정보를, `Access-Control-Allow-Methods`에는 허용하는 메서드를, `Access-Control-Allow-Header`에는 사용 가능한 헤더 목록을, `Access-Control-Max-Age`에는 현재의 preflight request를 브라우저가 캐싱 가능한 최대 시간을 담아서 제공합니다.

**Simple Request**

하지만 이런 preflight request를 보내지 않는 경우도 있습니다. 우선 브라우저를 쓰지 않으면 보내지 않는데요, 앞서 말했듯이 origin이 다른지 판단하는 것은 브라우저 스펙이기 때문입니다. 그래서 Postman과 같은 기능을 사용하면 CORS 문제가 발생하지 않습는다. 하지만 브라우저에서도 preflight request를 생략하는 경우가 있는데, 이를 `simple request`라고 합니다. simple request는 아무 때나 보낼 수 있는 것은 아니고 다음의 세 가지 조건을 만족해야 합니다.

- 본 요청 메서드가 `GET`, `HEAD`, `POST` 중 하나일 것
- 클라이언트에서 자동으로 넣어주는 헤더와 Fetch 표준 정책에서 정의한 `CORS-safelisted request header`라는 헤더 목록에 들어 있는 헤더 외에 다른 헤더를 수동으로 넣어주지 않았을 것
    - CORS-safelist request Header
        - Accept
        - Accept-Language
        - Content-Language
        - Content-Type
- Content-Type의 경우 다음의 값들만 있을 것
    - application/x-www-form-urlencoded
    - multipart/form-data
    - text/plain

이 경우에는 preflight 요청을 보내지 않고 서버가 본 요청에 대한 응답 헤더에 CORS 관련된 헤더를 보내서 브라우저가 이를 검사하는 형태로 CORS 정책 위반 여부를 검사합니다.

# CORS 에러 해결 방법

### 1. **@CrossOrigin 어노테이션 사용하기**

메소드 레벨 및 글로벌 레벨에서 srping mvc 애플리케이션에서 spring cors를 지원하는 방법이다. sprign mvc는 `@CorssOrigin` 어노테이션을 제공한다. 이 어노테이션은 어노테이션이 달린 메소드 또는 타입을 교차 출처를 허용하는 것으로 표시한다.

기본적으로 `@CrossOrigin`은 모든 출처, 모든 헤더, `@RequestMapping` 주석에 지정된 Http 메소드에 최대 30분을 허용한다. 어노테이션에 속성 값을 넣어 기본 값을 대체할 수 있다.

속성값을 살펴보면,

- `origins`
    - 허용된 출처, 이 값은 pre-flight 응답과 실제 응답 모두에 access-control-allow-origin헤더에 배치된다.
- `allowedHeaders`
    - 실제 요청 중에 사용할 수 있는 요청 헤더 목록이다. pre-flight의 응답 헤더인 access-control-allow-header에 값이 사용된다.
- `allowCredential`
    - 브라우저가 요청과 관련된 쿠키를 포함해야 되는지 여부를 결정한다.
    - 이 값이 true이면, pre-flight 응답에는 값이 true로 설정된 access-control-allow-credentials 헤더가 포함된다.

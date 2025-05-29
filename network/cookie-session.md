# Cookie와 Session
---

## Cookie(HTTP Cookie, Web Cookie, Browser Cookie)
: 서버가 사용자의 웹 브라우저에 전송하는 작은 **데이터 조각**으로 요청이 동일한 브라우저에서 들어왔는지 아닌지를 판단할 때 주로 사용한다.



#### 특징

- 쿠키는 브라우저 단위로 생성한다
- 다른 도메인이 대신하여 쿠키 발급이 불가능하다
- 만료 시간까지 상태 정보를 유지한다



#### Cookie의 목적

1. **Session Management**
   <br>
   : 서버에 저장해야 할 로그인, 장바구니, 게임 스코어 등의 정보를 관리한다
2. **Personalization** <br>
   : 사용자 선호, 테마 등 세팅
3. **Tracking**
   <br>
   : 사용자 행동을 기록하고 분석하는 용도


#### Cookie의 구조와 속성
기본적으로 key-value 형태로 구성된다.

|구성 요소||
|----------|----------------------------------------------------------------------------|
|Key|쿠키를 구분하는 고유 키|
|Value|저장할 데이터|
|Domain|쿠키가 전송하게 될 호스트|
|Path|URL 내에 반드시 존재해야 하는 URL 경로|
|LifeTime|쿠키의 만료 시점을 설정(Expires, Max-Age)|
|보안속성|HTTPS로만 전송되거나 JavaScript에서 접근하지 못하도록 설정(Secure, HttpOnly)|

<br>

```
Set-Cookie: sessionId=abc123; Path=/; Domain=example.com; Secure; HttpOnly
```

#### Cookie의 동작 원리

1. **Set-Cookie Header** <br>
  - 서버는 HTTP 응답에 Set-Cookie 헤더를 포함시켜 브라우저에 쿠키를 설정한다.
  - Set-Cookie: user=JohnDoe; Path=/; Max-Age=3600; HttpOnly
2. **전송** <br>
  - 브라우저는 쿠키를 요청 시 Cookie 헤더에 포함해 서버로 전송한다.
  - Cookie = user=JohnDoe
3. **클라이언트 저장** <br>
  - 사용자의 브라우저가 쿠키를 저장하며 사용자는 이를 브라우저 설정에서 확인하거나 삭제할 수 있다.


![image](https://github.com/user-attachments/assets/fc8eda87-e3a9-41f5-a62e-65d8e74ed78e)
![image](https://github.com/user-attachments/assets/1cc83344-9d9e-4e77-a584-f172d100c277)


클라이언트에게 쿠키를 저장하라고 전달
```
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: yummy_cookie=choco
Set-Cookie: tasty_cookie=strawberry

[page content]
```


서버로 전송되는 모든 요청과 함께 브라우저는 저장했던 쿠키 회신
```
GET /sample_page.html HTTP/1.1
Host: www.example.org
Cookie: yummy_cookie= choco; tasty_cookie=strawberry
```

<br>

#### Cookie의 유형

- Session Cookie: 브라우저 종료 시 삭제되는 임시 쿠키, 로그인 상태 유지에 사용
- Permanent Cookie: 특정 유효기간까지 유지되며, 사용자 설정(언어, 테마 등)을 기억한다.
- Security Cookie: HTTPS 연결에서만 전송되며, 민감한 정보를 보호한다.
- HttpOnly Cookie: JavaScript 접근을 차단하여 보안성을 높인다.

<br>

---

## Session
: 클라이언트와 서버 간의 상태 정보를 유지하는 방법으로 서버가 클라이언트의 상태 정보를 저장하고 요청이 들어올 때마다 상태 데이터를 확인한다


1. 클라이언트가 TCP 연결을 수립한다.
2. 클라이언트는 요청을 전송한 뒤 응답을 기다린다.
```
GET / HTTP/1/1
Host: developer.mozilla.org
Accept-Language: fr

---
POST /contact_form.php HTTP/1.1
Host: developer.mozilla.org
Content-Length: 64
Content-Type: application/x-www-form-urlencoded

name=Joe%20User&request=Send%20me%20one%20of%20your%20catalogue
``` 
3. 서버는 요청에 대해 처리하고 그에 대한 응답을 상태 코드 그리고 요청에 부합하는 데이터와 함께 돌려보낸다.
```
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html

<!DOCTYPE html... (here comes the 29769 bytes of the requested web page)
```

<br>

![image](https://github.com/user-attachments/assets/1f4e93ee-adbd-4dfe-9040-0d190c6c0598)
![image](https://github.com/user-attachments/assets/750f530a-3c62-46d3-a2e3-22f57676fa70)
![image](https://github.com/user-attachments/assets/391c0c84-1e0b-4174-97ea-c38ed8a12ce8)


## Session과 Cookie의 차이점
| **특성**      | **쿠키 (Cookie)**                       | **세션 (Session)**                          |
| ----------- | ------------------------------------- | ----------------------------------------- |
| **저장 위치**   | 클라이언트(사용자의 브라우저)                      | 서버 (세션 데이터 저장소)                           |
| **보안성**     | 데이터가 클라이언트에 저장되므로 상대적으로 취약            | 데이터가 서버에 저장되므로 상대적으로 안전                   |
| **속도**      | 로컬 저장으로 인해 읽기 속도가 빠름                  | 서버 요청이 필요하므로 느림                           |
| **데이터 크기**  | 브라우저마다 제한 (약 4KB)                     | 서버 저장소에 따라 제한이 없거나 유연하게 확장 가능             |
| **데이터 지속성** | 만료시간(expiry time)을 설정 가능 (Persistent) | 브라우저 종료 또는 세션 만료 시 사라짐 (Transient)        |
| **생명주기**    | 브라우저 설정에 따라 유지 (사용자가 쿠키를 삭제할 수도 있음)   | 브라우저를 닫거나 서버에서 세션을 만료시키면 종료               |
| **사용 목적**   | 상태 유지, 세션 ID 전달, 사용자 설정 정보 저장         | 사용자 인증, 개인화된 데이터 저장, 서버에서 상태 관리           |
| **사용 사례**   | - 로그인 상태 유지<br>- 방문 기록<br>- 사이트 설정 저장 | - 로그인 정보 관리<br>- 장바구니 관리<br>- 사용자별 맞춤 서비스 |

----

<br>

## 면접 질문

<details>
  <summary>❓ 쿠키와 세션을 사용하는 이유는</summary>
  
 Http 프로토콜의 특징이자 약점을 보안하기 위해서 사용한다. <br>
 Connectionless, Stateless
  
</details>

<details>
  <summary>❓ 쿠키와 세션의 차이는</summary>
  
 쿠키와 세션은 비슷한 역할을 하며 동작 원리도 비슷하다. 그 이유는 세션도 결국 쿠키를 사용하기 때문이다. <br>
 둘의 큰 차이는 사용자의 정보가 저장되는 위치이다.
  
</details>

<details>
  <summary>❓ 세션을 사용하면 되는데 쿠키를 사용하는 이유는</summary>
  
 세션이 쿠키에 비해 보안이 높은 편이나 쿠키를 사용하는 이유는 쿠키가 서버 자원의 낭비를 방지하고 웹사이트의 속도를 높일 수 있기 때문이다
  
</details>

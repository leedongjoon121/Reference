# 웹 브라우저에 URL을 입력하면 일어나는 과정

#### <a href="http://owlgwang.tistory.com/1"> reference </a>

## 흔히 쓰는 웹 브라우저(Chrome, Internet Explore, Firefox)에 URL(Uniform Resource Locater)을 입력하고 Enter를 칠때, 웹페이지가 보여지는 과정

### 1. 주소표시줄에 URL을 입력하고 Enter를 입력한다.

### 2. 웹 브라우저가 URL을 해석한다.
- url 구조

```
  scheme : [//[user:password@]host[:port]][/]path[?query][#fragment]
  
```

#### url 문법
- 1. 제일 앞에 자원에 접근할 방법을 정의해 둔 프로토콜 이름을 적는다.  (http, telnet, gopher, usenet 등)
- 2. 프로토콜 이름 다음에는 프로토콜이름을 구분하는 구분자인 ":"을 적는다.
- 3. 만약 IP혹은 Domain name 정보가 필요한 프로토콜이라면 ":" 다음에 "//"를 적는다.
- 4. 프로토콜 구분자인 ":" 혹은 "//" 다음에는 프로토콜마다 특화된 정보를 넣는다.

```
예1) http://www.somehost.com/a.gif- IP 혹은 Domain name 정보가 필요한 형태 ( www.somehost.com에 있는 a.gif를 가리키고 있음 )
예2) ftp://id:pass@192.168.1.234/a.gif- IP 혹은 Domain name 정보가 필요한 형태 ( 192.168.1.234에 있는 a.gif를 가리키고 있음 )
예3) mailto:somebody@mail.somehost.com - IP정보가 필요없는 프로토콜 ( mailto 프로토콜은 단지 메일을 받는 사람의 주소를 나타냄 )
```
- 5. 만약 url이 문법에 맞지 않는다면 입력을 웹 브라우저의 기본 검색엔진으로 검색을 요청한다.

### 3. URL이 문법에 맞으면 Punycode encoding을 url의 host부분에 적용한다.
```
Punycode : 비영어권의 언어로 이루어진 도메인 주소는 (네임)서버나 웹에서 제대로 인식을 하지 못하기 때문에, 이를 제대로 인식할 수 있도록 변환해 주어야 한다. 이때 사용되는 코드가 아스키를 기반으로 만들어진 퓨니코드(PunyCode)이다.

```

### 4. HSTS (HTTP Strict Transport Security)목록을 로드해서 확인한다.
```
  HSTS (HTTP Strict Transport Security) 란?  기존의 https 보다 더 강화된 보안 정책
   - HTTP 대신 HTTPS만을 사용하여 통신해야 한다고 웹 사이트가 웹 브라우저에 알리는 보안 기능.
```
일반적으로 https를 강제하게 될때 서버측에서 302 Redirect를 이용하여 전환시켜줄 수 있다. 하지만 이것이 취약점 포인트로 작용 될 수 있다.


## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/http1.png?raw=true)

그렇기 때문에, 클라이언트(브라우저)에게 HTTPS를 강제 하도록 하는 것이 권장되는데, 이것이 HSTS이다. 클라이언트 (브라우저)에서 강제 하기 때문에 Plain Text인 Http를 이용한 연결 자체가 최초부터 시작되지 않으며 클라이언트 측에서 차단되는 장점이 있다.

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/http2.png?raw=true)

사용자가 최초로 사이트에 접속을 시도하면 웹서버는 HSTS설정에 대한 정보를 브라우저에게 응답하게 된다. 브라우저는 이 응답을 근거로 일정시간(max-age)동안 HSTS 응답을 받은 웹사이트에 대해서 https접속을 강제화 하게 된다.


### 5. DNS(Domain Name Server)를 조회한다. 
1. DNS에 요청을 보내기 전에 먼저 Browser에 해당 Domain이 cache되어 있는지 확인한다. 
2. 없을 경우 로컬에 저장되어 있는 host파일에서 참조할 수 있는 Domain이 있는지 확인한다.
3. 1번 / 2번 모두 실패했을 경우, Network stack에 구성되어 있는 DNS로 요청을 보낸다. (DNS는 일반적으로 Local router, ISP의 캐싱 DNS)

### 6. ARP(Address Resolution Protocol)로 대상의 IP와 MAC address를 알아 낸다.

### 7. 대상과 TCP 통신을 통해 Socket을 연다.

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/tcp1.png?raw=true)

1) 브라우저가 대상 서버의 IP 주소를 받으면 URL에서 해당 포트 번호(HTTP의 기본값은 80, HTTPS의 기본값은 443)를 가져와서, TCP Socket stream 요청

2) TCP segment가 만들어지는 Transport Layer(OSI Model Layer 4)로 전달. 대상 포트 header에 추가되고 source port는 시스템에서 동적 포트 범위내에서 임의 지정

3) TCP segment를 Network Layer(OSI Model Layer 3)로 전달. segment header에 대상 컴퓨터의 IP주소와 현재 컴퓨터의 IP주소가 삽입된packet 구성

4) packet이 Link Layer(OSI Model Layer 2)로 전달. 시스템의 MAC address와 gateway(local router)의 MAC주소를 포함하는 Frame header 추가 (gateway의 MAC address를 모르는경우 ARP를 이용해 찾아야 한다.)

5) packet이 ethernet, Wifi, Cellular data network 중 하나로 전송 

- 광인터넷을 쓸 경우 modem을 통해 광신호로 변경된 후 network node로 직접 전송

6) packet local subnet router 도착, AS(Autonomous System)경계 router들을 통과

- 해당 라우터에선 packet의 IP header에서 target address를 추출하여 적당한 다음 hop으로 routing IP header의 TTL(Time To Live)필드는 통과하는 라우터의 대해 하나씩 감소
- TTL필드가 0이 되거나 현재 router 대기열에 공간이 없으면 네트워크 정체로 packet 삭제

7) TCP Socket 통신과정

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/tcp2.jpg?raw=true)

### 8. HTTPS인 경우 TLS (Transport Layer Security) handshake가 추가된다.
- TLS는 SSL(Secure Sockets Layer)이 표준화 되면서 바뀐 이름이다. HTTPS로 통신을 하게 되면 7번 TCP Socket 통신과정 전에 아래 그림과 같은 통신이 추가 된다. 

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/tcp3.PNG?raw=true)

0~28ms : TCP socket 생성 - TLS는 TCP 통신으로만 전송 되기 때문에 일단 TCP socket이 생성 돼야 한다. 

56ms : TCP 연결을 통해 클라이언트는 실행 중인 TLS protocol의 버전, 사용가능한 암호 세트, 사용할 수 있는 TLS 옵션 목록 등을 평문으로 보낸다.

84ms : 서버는 통신할 때 사용 할 TLS의 버전을 선택하고, 클라이언트가 제공한 목록에서 암호 조합을 결정하고 인증서를 첨부해서 클라이언트에 보낸다. 선택적으로 서버는 다른 TLS 확장에 대한 클라이언트 인증서 및 매개 변수에 대해 요청을 보낼 수도 있다.

112ms : 양측이 공통된 버전과 암호를 협살 할 수 있고, 클라이언트가 서버에서 제공한 인증서에 만족하면, 클라이언트는 RSA 또는 Diffie-hellman 키 교환을 시작한다. 이 교환은 이어지는 세션에서 사용할 대칭키를 설정한다.

140ms : 서버는 클라이언트가 전송한 키 교환 매개변수를 처리하고 MAC address을 확인하여 메시지 무결성을 검사하고 암호화 된 Finished message를 클라이언트에 전송한다.

168ms : 클라이언트를 협상 된 대칭키를 사용해 message 암호를 해독하고 MAC address를 확인해서 모두 정상이면 터널이 설정되고 통신을 시작한다.

※ 참고 : 처음 연결하는 TLS handshake는 위와 같이 2-RTT(Round Trip Time)이지만 최적화를 하면 1-RTT로 배포 할 수 있다. 

### 9. HTTP 프로토콜로 요청

### 10. HTTP 서버가 응답
- Httpd (Http Daemon) : 응답/요청을 처리하는 서버,
- 가장 일반적인 httpd서버는 Linux의 경우는 Apache 또는 Nginx,  Window의 경우는 IIS

1. httpd 서버가 요청을 수신
2. 서버는 요청을 다음 매개변수로 구분
- HTTP method (GET, POST, PUT, DELETE, CONNECT, OPTIONS, TRACE, HEAD) 이며, 주소표시줄에 직접 입력한 URL의 경우 GET으로 처리
- 도메인 (google.com)
- 요청된 경로 (/path)
3. 서버는 google.com에 해당하는 서버에 구성된 가상 호스트가 있는지 확인(하나의 서버에 여러 도메인을 서비스 할 수있음)
4. 서버는 google.com이 GET 요청을 수락할 수 있는지 확인
5. 서버는 클라이언트가 IP, 인증 등을 통해 이 method를 사용할 수 있는지 확인
6. 서버에 rewrite module이 설치 돼 있으면 (예 : Apache의 경우 mod_rewrite, IIS의 경우 URL Rewrite) 요청 된 rule 중 하나와 일치하도록 시도, 일치하는 rule 이 있는 경우 서버는 해당 rule을 사용하여 요청을 다시 작성
7. 서버는 요청에 해당하는 콘텐츠를 가져오고, 여기서는 "/"가 기본 경로이므로 이 경우 index파일을 해석
8. 서버는 핸들러에 따라 파일을 구문 분석한다. php인 경우는 php를 사용하여 index파일 해석 후 출력을 클라이언트로 스트리밍

### 11. 웹 브라우저가 그린다.

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/dom.png?raw=true)

```
웹 브라우저의 기능은 서버에서 요청하고 브라우저 창에 표시하여 선택한 웹 리소스를 표시하는 것이다. 리소스는 일반적으로 HTML문서이지만 PDF, 이미지 또는 다른 유형의 콘텐츠일 수도 있다. 자원의 위치는 URI(Uniform Resource Identifier)를 사용하여 사용자가 지정한다.
브라우저가 HTML파일을 해석하고 표시하는 방법은 HTML 및 CSS 사양에 지정되어 있다. 이 사양은 웹 표준 단체인 W3C(World Wide Web Consortium)에서 관리한다.
```

#### 1.브라우저의 일반적인 User Interface 요소
- URI를 입력하기 위한 주소표시줄
- 뒤로 및 앞으로 버튼
- 북마크 버튼
- 새로고침 및 중지 버튼
- 홈페이지 이동 버튼


#### 2.브라우저 자세한 구조
- User InterFace : 사용자 인터페이스는 주소 표시줄, 뒤로 / 앞으로 버튼, 북마크 메뉴 등 포함. 요청한 페이지가 표시된 창을 제외하고 브라우저의 모든 부분
- Browser Engine : Browser Engine은 UI와 Rendering Engine 사이의 작업을 통제
- Rendering Engine : Rendering Engine은 요청된 콘텐츠를 표시한다. HTML의 경우 Rendering Engine은 HTML과 CSS를 구문 분석하고 파싱된 컨텐츠를 화면에 표시
- Networking : Networking은 인터페이스와 독립적으로 구현되어 HTTP 요청과 같은 Network호출을 처리
- UI backend : UI backend는 콤보 상자 및 창과 같은 기본 위젯을 그리는 데 사용. 특정 플랫폼이 아닌 일반 인터페이스 제공. 운영체제 사용자 인터페이스 method 사용
- Javascript Engine : Javascript 코드를 구문 분석하고 실행하는 데 사용.
- Data Storage : 브라우저는 쿠키와 같이 모든 종류의 데이터를 로컬로 저장해야 할 수도 있음. localStorage, IndexedDB, WebSQL, File System과 같은 저장 수단을 지원

#### 3.HTML parsing
- 렌더링 엔진은 요청 된 문서의 내용을 네트워킹 계층에서 가져옴. 보통 8Kb단위로 이루어짐
- HTML의 마크업을 parse tree로 만드는 HTML parser의 기본 작업
- 생성된 트리(parse tree)는 DOM(Document Object Model)노드와 속성 노드의 트리이다. Javascript와 같이 HTML문서의 객체 표현과 HTML 요소의 인터페이스 이고, 트리의 root는 "Documnet"객체이다. 스크립팅을 통한 조작 전에는 마크업과 DOM은 거의 일대일 관계를 유지

#### 4.Parsing 알고리즘
- HTML은 regular top-down 방식이나 bottom-up parsers를 사용할 수 없음
- 이유 
 1) 관대한 언어이다.
 2) 브라우저는 잘못된 HTML을 지원하기 위해 일반적인 오류 허용 범위를 갖고 있다.
 3) HTML이 파싱되는 동안 변경될 가능성이 있다.(document.write()를 사용해서 동적 코드로 토큰을 추가할 수 있다.)

- 일반적인 parsing 기술을 사용할 수 없이 때문에 HTML을 구문 분석하기 위한 사용자 정의 parser를 사용. 구문분석 알고리즘은 HTML5 사양에 자세히 명세돼 있음.
- 이 알고리즘은 토큰화와 트리구조화의 두 단계로 구성


#### 5.구문분석이 끝나면 브라우저는 페이지에 연결된 외부 리소스(CSS, Image, Javascript file)를 가져 온다. 
이 단계에서 브라우저는 분서를 대화형으로 표시하고 문서가 구문 분석 된 후에 실행되어야 하는 "deferred"모드의 스크립트를 구문 분석한다. 문서 상태가 "complete"로 설정 되고 "load"이벤트가 발생한다. HTML 페이지에는 "Invalid Syntax"오류가 없다. 브라우저가 잘못된 콘텐츠를 고쳐서 계속한다.

#### 6.CSS parsing
- "CSS lexical and syntax grammar"를 사용하여 CSS파일, <style>태그 내용 및 style 속성 값을 parsing한다.
- 각 CSS file은 StyleSheet object로 parsing된다. 각 object에는 CSS문법에 해당하는 선택자와 객체가 일치하는 CSS 문법이 있다.
- CSS parser는 regular top-down 방식이거나 bottom-up parsers일 수 있다.

#### 7. Page Rendering
  1) DOM 노드를 탐색하고 각 노드에 대한 CSS 값을 계산하여 "Frame tree" 또는 "Render tree"를 만듦.
  2) 자식 노드의 width와 수평 margin, border, padding 을 합해서 Frame tree의 아래쪽에 있는 각 노드의 기본 너비를 계산.
  3) 각 노드의 사용 가능한 너비를 자식 노드에 할당하여 각 노드의 실제 width 값 계산.
  4) 텍스트 배치를 적용하고 하위 노드의 height와 margin, border, padding을 합해 각 노드의 높이를 상향식으로 계산.
  5) 위에서 계산 된 정보를 사용해서 각 노드의 좌표를 계산.
  6) float, absolutely, relatively 와 같은 속성이 사용되었을 경우 더 복잡한 단계가 수행 된다. 
      자세한건  http://dev.w3.org/csswg/css2/ 와 http://www.w3.org/Style/CSS/current-work 참조
  7) 페이지의 어느 부분을 그룹으로 애니메이션화 할 수 있는지 설명하는 레이어를 만듦. frame/render object는 layer에 할당
  8) 텍스처는 페이지의 각 레이어에 할당
  9) 각 frame/render object를 통해서 각 레이어 별로 그리기 명령을 실행.
  10) 위의 모든 단계를 웹페이지가 렌더링 된 마지막 시간에 계산 된 값을 재사용 할 수 있으므로 점진적 변경은 작업이 덜 필요하다.
  11) 페이지 레이어는 합성 프로세스로 보내져 browser chrome, iframe, addon panels과 같은 시각적인 레이어와 결합된다.
  12) 최종 레이어 위치가 계산되고 Direct3D / OpenGL을 통해 합성 명령이 실행된다. GPU 명령 버퍼는 비동기 렌더링을 위해 GPU로 출력되고 frame은 window server로 전송된다.

  
#### 8.GPU rendering
- 렌더링 프로세스 동안 graphical computing layers는 CPU 또는 GPU를 사용할 수 있다.
- graphical rendering 계산에 GPU를 사용하는 경우 그래픽 소프트웨어 레이어에서 작업을 여러조각으로 분할하여 렌더링 프로세스에 필요한 부동 소수점 계산을 위해 GPU 대용량 병렬 처리를 사용 할 수 있다.


렌더링이 완료된 후 브라우저는 Javascript 실행을 통해 DOM과 CSSOM이 변경 될 수 있는데 레이아웃이 수정 되는 경우 페이지 렌더링 및 페인팅을 다시 수행한다.

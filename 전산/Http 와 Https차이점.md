# Http와 Https 차이점

### HTTP 
- HyperText Trnasfer Protocol 로서, WWW 상에서 정보를 주고 받는 프로토콜
- 클라이언트인 웹 브라우저가 서버에 HTTP를 통해 웹페이지나 이미지 정보를 요청하면 서버는 이 요청에 응답하여 요구하는 정보를 제공
=> 결국 HTTP는 웹브라우저(Client)와 서버(Server)간의 웹페이지 같은 자원을 주고 받을 때 쓰는 통신 규약
- http는 텍스트 교환이다, html 페이지도 텍스트다. 바이너리 데이터로 되어 있는 것도 아니고 단순 텍스트를 주고 받기 때문에 누군가 
  네트워크에서 신호를 가로채어 본다면 내용이 노출된다.

### HTTPS
- http와 통신 내용을 암호화 하는 것과 다르다.
- S : Secure Socket, 보안 통신망을 말한다.
- 공개키 암호화 방식 이다.

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/%EA%B3%B5%EA%B0%9C%ED%82%A4.PNG?raw=true)

공개키 알고리즘은 암호화, 복호화시킬 수 있는 서로 다른 키 2개가 존재하는데, 이 두개의 키는 1번키로 암호화 -> 반드시 2번키로 복호화
2번키로 암호화 -> 반드시 1번키로 복호화 할수 있는 룰이 존재한다.

그 중 하나의 키는 모두에게 공개키로 공개키 저장소에 등록해 놓고, 그 누구에게도 알려주지 않고 개인(서버)만 알고 있는 개인키를 서버가 소유해서 통신하는 방식

이렇게 해서 클라이언트는 공개키를 얻은 인증된 사용자가 암호화해서 정보를 보낼 수 있고, 서버는 개인키로 해독하여 요청에 대해 처리할 수 있게 된다.

또한 서버가 정보를 제공할 때 개인키로 암호화를 하기 때문에 공개키가 있는 누구나 정보를 알 수 있지만, 대신 공개키로 복호화 할 수있다는 점을 통해 해당 서버에서 개인키로 암호화 했다는 것을 보장할 수 있다.

### 결국 HTTPS는 인터넷 상에서 정보를 암호화 하는 SSL (Secure Socket Layer)프로토콜을 이용하여 웹브라우저(클라이언트)와 서버가 데이터를 주고받는 통신규약 이다.


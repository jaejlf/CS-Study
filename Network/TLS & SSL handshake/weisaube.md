# TLS & SSL Handshake

# A. TLS & SSL Handshake란?

> TLS 암호화를 사용하는 통신 세션을 실행하는 프로세스. SSL 또는 TLS 클라이언트와 서버가 통신하는 비밀 키를 설정할 수 있다.

<br/>

통신 양측은 TLS 핸드셰이크 중에 메시지를 교환하여 1)서로를 인식하고, 2)서로를 검증하며, 3)사용할 암호화 알고리즘을 구성하고, 4)세션 키를 합의한다.

SSL은 오래 전에 TLS(Transport Layer Security)로 대체되기에, SSL 핸드셰이크란 이름이 아직 널리 사용되고 있지만, 이제는 TLS 핸드셰이크로 불린다.

<br/>

## 1. 용어 정리 👉 SSL, TLS

<br/>

### 📌 SSL(Secure Sockets Layer, 보안 소켓 레이어)

> 서버 및 브라우저의 표준 인터넷 프로토콜로, 암호화된 연결을 생성한다

인터넷 통신의 개인정보 보호, 인증, 데이터 무결성을 보장하기 위해 Netscape가 1995년 처음으로 개발하였다. SSL은 현재 사용 중인 TLS 암호화의 전신이다.

<br/>

### 📌 TLS(Transport Layer \***\*Security\*\***, 전송 계층 보안)

> 인터넷 커뮤니케이션을 위한 개인 정보와 데이터 무결성을 제공하는 보안 프로토콜

웹 사이트를 로드하는 웹 브라우저와 같이 웹 응용 프로그램과 서버 간의 커뮤니케이션을 **암호화**한다.

TLS는 또한 이메일, 메시지, 보이스오버 IP(VoIP)와 같은 다른 커뮤니케이션을 암호화하기 위해 사용된다.

Netscape가 개발한 SSL(Secure Socket Layer)에 기반한 기술이다.

<br/>

#### **SSL/TLS 프로토콜의 역할**

✔️ 암호화, 인증, 무결성

- 암호화: 제 3자로부터 전송되는 데이터를 숨긴다
- 인증: 정보를 교환하는 당사자가 요청된 당사자인지 확인
- 무결성: 데이터가 위조되거나 변조되지 않았는지 확인

<br/>

+) TLS와 HTTPS의 차이

HTTPS는 HTTP 프로토콜 상위에서 TLS 암호화를 구현한 것으로 모든 웹 사이트와 다른 웹 서비스에서 사용된다.

<br/>

## 2. 용어 정리(복습) 👉 대칭키 암호화, 공개키 암호화

### 📌 대칭키 암호화(symmetric-key algorithm)

> 암호화와 복호화에 같은 암호키(대칭 키)를 사용

<br/>

### 📌 비대칭키(Asymmetric Key) = 공개키(Public Key)

> 암호화와 복호화에 사용하는 암호키를 분리

<br/>

공개키 암호화 방식에서 사용하는 대표적인 키 교환 알고리즘: `RSA` 알고리즘, `Diffie-Hellman` 알고리즘

<br/>
<aside>
💡 TLS 핸드셰이크의 정확한 단계는 사용되는 키 교환 알고리즘의 유형과 커뮤니케이션 양측에서 모두 지원하는 암호 제품군의 유형에 따라 달라지나, 대부분 RSA 키 교환 알고리즘이 사용된다.
</aside>

모든 TLS 핸드셰이크가 비대칭 암호화(공개 키와 개인 키)를 사용하지만,세션 키를 생성하는 과정에서 모두가 개인 키를 사용하는 것은 아니다.(ex. Diffie-Hellman)

<br/>

## 3. 용어 정리 👉 CA와 SSL 인증서

<br/>

### 📌 SSL 인증서

> SSL을 실행시킬 수 있는 인증서

<br/>

SSL은 SSL 인증서(공식적으로 "TLS 인증서")가 있는 웹사이트만 실행할 수 있다.

SSL 인증서는 웹사이트나 애플리케이션 서버가 웹에 저장하고 표시한다.

<br/>

### 📌 CA(Certificate Authority)

> 인증 기관은 다른 곳에서 사용하기 위한 디지털 인증서를 발급하는 하나의 단위

<br/>

CA(인증 기관)는 SSL 인증서 발행을 담당한다.

<br/>

# B. TLS & SSL Handshake의 단계

### 발생 시기

사용자가 HTTPS를 통해 웹 사이트를 탐색하고 **브라우저가 처음 해당 웹 사이트의 원본 서버
를 쿼리하기 시작**할 때마다 발생.

TLS 핸드셰이크는 TCP 연결이 TCP 핸드셰이크를 통해 열린 후에 발생한다.

<br/>

### 발생 단계

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/5aYOr5erfyNBq20X5djTco/3c859532c91f25d961b2884bf521c1eb/tls-ssl-handshake.png)

<br/>

1. ClientHello
   - 클라이언트가 서버에 연결을 시도하며 전송하는 패킷
   - 클라이언트가 지원하는 TLS 버전, 지원되는 암호 제품군, 그리고 "클라이언트 무작위"라고 하는 무작위 바이트 문자열이 포함된다.

<br/>

2. ServerHello
   - ClientHello 메세지에 대한 응답
   - 서버가 서버의 SSL 인증서, 서버에서 선택한 암호 제품군, 그리고 서버에서 생성한 또 다른 무작위 바이트 문자열인 "서버 무작위"를 포함하는 메시지를 전송

<br/>

3. Certificate
   - 서버가 자신의 SSL 인증서를 클라이언트에게 전달. 인증서 내부에는 서버가 발행한 공개 키 (개인 키는 따로 서버가 소유)가 들어있다.
   - 클라이언트는 서버의 SSL 인증서를 인증서 발행 기관(CA)을 통해 검증

<br/>

4. Server Key Exchange / ServerHello Done
   - 서버의 공개 키가 SSL 인증서 내부에 없는 경우, 서버가 직접 전달
   - 공개키가 SSL 인증서 내부에 있는 경우 `Server Key Exchange` 는 생략됨

<br/>

5. ClientKeyExchange
   - 클라이언트는 **데이터 암호화에 사용할 대칭 키를 생성**한 후 SSL 인증서 내부에서 추출한 서버의 공개 키를 이용해 암호화한 후 서버에게 전달
   - 여기서 전달된 대칭키가 TSL Handshake의 데이터를 실제로 암호화할 대칭키

<br/>

6. ChangeCipherSpec/Finished
   - ChangeCipherSpec 패킷은 클라이언트와 서버 모두가 서로에게 보내는 패킷으로, 교환할 정보를 모두 교환한 뒤 통신할 준비가 다 되었음을 알리는 패킷
   - Finished 패킷을 보내어 SSL Handshake를 종료

<br/>

### 발생 단계 정리

<br/>

- 서버는 CA에 사이트 정보와 공개 키를 전달하여 인증서를 받음
- 클라이언트는 브라우저에 CA 공개 키가 내장되어 있다고 가정
- ClientHello(암호화 알고리즘 나열 및 전달)
- ServerHello(암호화 알고리즘 선택)
- Server Certificate(인증서 전달)
- Client Key Exchange(데이터를 암호화 할 대칭 키 전달)
- Client / ServerHello done (정보 전달 완료)
- Finished(SSL Handshake 종료)

<br/>

# C. 참고자료

🔗 [TLS & SSL Handshake](https://steady-coding.tistory.com/512)

🔗 [TLS 핸드셰이크란 무엇일까요?](https://www.cloudflare.com/ko-kr/learning/ssl/what-happens-in-a-tls-handshake/)

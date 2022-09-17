# 💡 TLS/SSL HandShake


TLS/SSL HandShake 란, `HTTPS` 에서 클라이언트와 서버간 통신 전 SSL 인증서로 신뢰성 여부를 판단하기 위해 연결하는 방식을 말한다.

<br/>

> #### 🔖 TLS 핸드셰이크와 SSL 핸드셰이크
> `SSL(Secure Sockets Layer)` 은 원래 HTTP용으로 개발된 암호화 프로토콜로, 오래 전에 `TLS(Transport Layer Security)` 로 대체되었다. 
> 
> SSL 핸드셰이크는 "SSL"이라는 이름이 아직 널리 사용되고 있지만, 이제는 TLS 핸드셰이크로 불린다.

<br/>

## TLS HandShake는 언제 발생할까?

TLS 핸드셰이크는 사용자가 `HTTPS`를 통해 웹 사이트를 탐색하고 브라우저가 처음 해당 웹 사이트의 원본 서버를 쿼리하기 시작할 때마다 발생한다. 

다른 통신이 API 호출 및 HTTPS를 통한 DNS 쿼리를 포함하는 HTTPS를 사용할 때에도 항상 TLS 핸드셰이크가 발생한다.

TLS 핸드셰이크는 **TCP 연결이 TCP 핸드셰이크를 통해 열린 후**에 발생한다.

<br/>

## TSL HandShake 진행 순서

![](https://velog.velcdn.com/images/wisdom-one/post/32e6d97d-b3ac-4728-92bc-b2444e06286c/image.png)

TLS 핸드셰이크의 정확한 단계는 사용되는 키 교환 알고리즘의 유형과 커뮤니케이션 양측에서 모두 지원하는 암호 제품군의 유형에 따라 달라진다.

대부분 `RSA 키 교환 알고리즘`이 사용되며 그 원리는 다음과 같다.


1. **client hello 메시지** <br/>
클라이언트가 서버로 "hello" 메시지를 전송하면서 핸드셰이크를 시작한다. <br/>
이 메시지에는 클라이언트가 지원하는 `TLS 버전`, `지원되는 암호 제품군`, 그리고 `client random` 라고 하는 무작위 바이트 문자열이 포함된다.

2. **server hello 메시지** <br/>
클라이언트 헬로 메시지에 대한 응답으로 서버가 서버의 `SSL 인증서`, 서버에서 선택한 `암호 제품군`, 그리고 서버에서 생성한 또 다른 무작위 바이트 문자열인 `server random` 를 포함하는 메시지를 전송한다.

3. **인증** <br/>
클라이언트가 서버의 SSL 인증서를 인증서 발행 기관을 통해 검증한다. <br/>
이를 통해 서버가 인증서에 명시된 서버인지, 그리고 클라이언트가 상호작용 중인 서버가 실제 해당 도메인의 소유자인지를 확인한다.

4. **예비 마스터 암호 (premaster secret)** <br/>
클라이언트가 "premaster secret"라고 하는 무작위 바이트 문자열을 하나 더 전송한다. <br/>
예비 마스터 암호는 `공개 키` 로 암호화되어 있으며, 서버가 `개인 키` 로만 해독할 수 있다. (클라이언트는 서버의 SSL 인증서를 통해 공개키를 받는다.)

5. **개인 키 사용** <br/>
서버가 예비 마스터 암호를 해독한다.

6. **세션 키 생성** <br/>
클라이언트와 서버가 모두 client random, server random, premaster secret 을 이용해 세션 키를 생성한다. <br/>
이때 모두 같은 결과가 나와야 한다.

7. **클라이언트 준비 완료** <br/>
클라이언트가 세션 키로 암호화된 "finished" 메시지를 전송합니다.

8. **서버 준비 완료** <br/>
서버가 세션 키로 암호화된 "finished" 메시지를 전송합니다.

9. **안전한 대칭 암호화 성공** <br/>
핸드셰이크가 완료되고, 세션 키를 이용해 통신이 계속 진행된다.

<br/>

## 🔖 참고
[TLS 핸드셰이크의 원리](https://www.cloudflare.com/ko-kr/learning/ssl/what-happens-in-a-tls-handshake/)

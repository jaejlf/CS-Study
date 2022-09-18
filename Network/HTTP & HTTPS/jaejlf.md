# 📍 HTTP

- HTTP(Hyper Text Transfer Protocol)
- 서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜로, `80번 포트`를 사용하고 있다.
- 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다.
- 상태를 가지고 있지 않는 Stateless 프로토콜이며 Method, Path, Version, Headers, Body 등으로 구성된다.
- 암호화 되지 않은 평문 데이터를 전송하는 프로토콜로, 보안 문제가 발생할 수 있다.

<br><br>

# 📍 HTTPS

- HTTPS(Hyper Text Transfer Protocol Secure)
- HTTP에 데이터 암호화가 추가된 프로토콜로, `443번 포트`를 사용하고 있다.
- `SSL 인증서`를 통해 데이터를 암호화한다 → 데이터를 암호화해서 전송하기 때문에, 중간에서 제 3자가 데이터를 가로채더라도 해독할 수 없다.
- 네트워크 상에서 중간에 제 3자가 정보를 볼 수 없도록 암호화를 지원하고 있다. (cf. [대칭키 & 공개키](https://github.com/jaejlf/CS_Study/blob/main/Network/%EB%8C%80%EC%B9%AD%ED%82%A4%20%26%20%EA%B3%B5%EA%B0%9C%ED%82%A4/jaejlf.md))
- HTTP와 달리 암호화/복호화 과정이 필요하기 때문에 HTTP보다 속도가 느리다.
- 구글에서 HTTPS 웹사이트에 가산점을 주고 또 사용자들이 안전하다고 생각하는 사이트를 더 많이 방문하기 때문에 검색 엔진 최적화(SEO)에서 혜택을 볼 수 있다.

<br>

## HTTPS를 사용하는 이유

1. 기밀성 : HTTPS는 인터넷과 같은 공공 매체에서 두 참여자 간의 통신을 보호한다.
2. 무결성 : HTTPS는 변조되지 않은 정보로 목적지에 도달하게 한다.
3. HTTPS를 통해 웹사이트의 진위 여부를 확인할 수 있다.

<br>

=> 즉, HTTP에 비해 `보안`이 뛰어나고, `검색 엔진 최적화` 혜택을 볼 수 있다는 장점이 있다.

<br>

💡 SSL(Secure Socket Layer) = 들어오고 나가는 데이터들을 암호화하는 보안 기능을 갖고 있는 보안 인증서 (cf. [SSL 통신 과정](https://github.com/jaejlf/CS_Study/blob/main/Network/TLS%20&%20SSL%20handshake/jaejlf.md))



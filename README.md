# spring-cloud-example-config

## config files for git url

> https://github.com/kihwankim/spring-cloud-example


### RSA key gen 방법

- 명령어

```bash
 keytool -genkeypair -alias apiEncryptionKey -keyalg RSA -dname "CN=kihwan kim, OU=API Development, O=spring.cloud-example.com, L=Seoul, C=KR" -keypass "test1234" -keystore apiEncryptionKey.jks -storepass "test1234"
```

- keytool : jdk에서 제공하는 로직
- alias : keytool의 다른 이름
- keyalg : 사용 알고리즘
- dname : 서명 정보
    - "CN=kihwan kim, OU=API Development, O=spring.cloud-example.com, L=Seoul, C=KR"
    - 위치, 서명자, Oranization 등등을 명세
- keypass : key password 설정
- keystore : keystore 이름 설정 -> jks 파일 (java keystore 파일)
- storepass : store password 설정

- 정보 식별

```bash
keytool -list -keystore apiEncryptionKey.jks -v
```

- 인증서로 export 방식
    - trustServer.cer 라는 공개키 발급
    - 인증서 파일 : trustServer.cer
```bash
 keytool -export -alias apiEncryptionKey -keystore apiEncryptionKey.jks -rfc -file trustServer.cer
```

- 인증서를 다시 jks형태로 변경
    - trustServer.cer를 publicKey.jks로 변경하는 과정
```bash
 keytool -import -alias trustServer -file trustServer.cer -keystore publicKey.jks
```

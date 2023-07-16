# Network

### HTTP(Hyper Text Transfer Protocol)
#
- 웹 상에서 클라이언트와 서버 간 데이터를 주고 받기 위한 프로토콜
- 상태 정보를 저장하지 않는 <b>Stateless</b> 및 클라이언트의 요청에 맞는 응답을 보낸 후 연결을 끊는 <b>Connectionless</b> 특징
    - 연결 상태 처리나 상태 정보를 관리할 필요가 없어 서버 디자인이 간단
    - 통신의 정보를 모르기 때문에 매번 인증 필요 
        - 해결방안: 쿠키, 세션 등

### HTTP Method
#
|종류|기능|
|-|-|
|GET|데이터 조회|
|POST|요청 데이터 처리, 주로 등록에 사용|
|PUT|리소스를 대체(덮어쓰기), 해당 리소스가 없으면 생성|
|PATCH|리소스 부분 변경 (PUT이 전체 변경, PATCH는 일부 변경)|
|DELETE|데이터 삭제|

<br/>

> \+ GET 메서드와 POST 메서드

> GET 메서드<br/>
> URL에 요청 정보를 붙여서 전송 →  POST 방식보다 보안상 취약<br/>
> 캐싱을 사용할 수 있어 POST 방식보다 빠름

> POST 메서드<br/>
> 요청 정보를 HTTP 패킷의 Body 안에 숨겨서 서버로 전송 → GET 방식보다 보안상 안전 <br/>
> 클라이언트: 데이터를 인코딩하여 서버로 전송 / 서버: 해당 데이터를 디코딩

<br/>

### RESTful API
#
REST
- HTTP URI를 통해 자원을 명시하고, HTTP METHOD를 통해 자원에 대한 CRUD를 적용하는 것을 의미
- 자원(URI) + 행위(HTTP Method) + 표현
  - 자원 : client는 URI를 이용해서 자원을 지정하고 해당 자원에 대한 조작을 server에 요청
  - 행위 : GET, POST, PUT, DELETE
  - 표현 : 일반적으로 JSON, XML를 통해 데이터를 주고 받음

API(Application Programming Interface)
- 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용하고 서로 데이터 교환을 가능하게 하는것

REST API
- REST 기반으로 서비스 API를 구현하는것

RESTful
- REST원리를 따르는 시스템을 RESTful 이라 지칭

<br>

### HTTP 상태 코드
#
- 1xx : 처리가 진행 중
- 2xx : 성공 응답
- 3xx : 리다이렉트, 요청을 완료하려면 추가적인 작업(페이지 이동)이 필요
- 4xx : 클라이언트 요청 오류
- 5xx : 서버 오류

<br/>

### HTTP와 HTTPS의 차이점
#
- HTTP
    - 평문 데이터를 전송하는 프로토콜
    - TCP와 직접 통신
- HTTPS
    - HTTP에 SSL(보안 소켓 레이어) 또는 TLS(전송 계층 보안)를 통한 세션 데이터 암호화가 추가된 프로토콜
    - HTTP는 SSL과 통신 + SSL이 TCP와 통신
    - 기밀성(사생활 보호), 데이터 무결성, ID 및 디지털 인증서를 사용한 인증을 제공

### HTTPS의 특징과 장단점
#
- 공개키(비대칭키) 알고리즘 방식 사용
    - 사용자의 데이터를 공개키로 암호화 → 데이터를 서버로 전송 → 서버의 개인키를 통해 복호화하여 요청 처리
- 장점
    - 네트워크 상에서 열람, 수정이 불가능하므로 안전
- 단점
    - 암호화를 하는 과정이 웹 서버에 부하
    - 설치 및 인증서를 유지하는데 추가 비용이 발생
    - HTTP에 비해 느린 속도
    - 인터넷 연결이 끊긴 경우, 웹 서버가 클라이언트(브라우저)의 신원을 확인하고 암호화된 연결을 설정하기 위한 재인증 시간이 오래 걸림

<br/>

### IP 주소 체계
#
||IPv4|IPv6|
|-|-|-|
|특징|현재 일반적으로 사용|IPv4의 주소 개수가 부족하여 만들어짐|
|표기 방식|8비트 씩 .을 기준으로 4단위|16비트씩 :을 기준으로 8단위|
|예시|123.45.67.88(10진수)|2001:0DB8:1000::::1111:2222(16진수)|

<br/>

### 공인(public) IP와 사설(private) IP의 차이
<img src="https://file.okky.kr/images/1552834443613.png" alt="public_private_ip" width="100%">
- 공인 IP: 중복되지 않는 단 1개의 IP 주소로 공유기가 인터넷과 통신하도록 하는 역할을 하는 외부 IP 주소
- 사설 IP
    - 일반 가정이나 회사 내 등에 할당된 네트워크 IP 주소
    - 라우터(공유기)에 의해 로컬 네트워크상의 PC나 장치에 할당
- 사설 IP 주소만으로는 인터넷에 직접 연결할 수 없고, 라우터를 통해 1개의 공인 IP를 할당하고, 라우터에 연결된 개인 PC는 사설 IP를 각각 할당 받아 인터넷에 접속

### DNS (Domin Name System)
#
도메인
- 네트워크 상에서 컴퓨터를 쉽게 식별할 수 있도록 문자(영문, 한글 등)로 만든 인터넷주소
DNS
- 컴퓨터를 식별하는 호스트명인 도메인을 실제 서버인 IP 주소와 연결 시켜주는 시스템

<br>

### TCP / UDP
#
||TCP|UDP|
|-|-|-|
|연결 방식|연결형(3-way handshake)|비 연결형|
|전송 순서|보장|보장 X|
|수신 여부 확인|O|X|
|신뢰성|높음|낮음|
|속도|느림|빠름|
|사용 예시|이메일, 파일 전송 등|속도가 중요한 서비스인 스트리밍 등|

<br/>

> TCP에서 신뢰성 보장을 위한 제어 기능

> TCP 흐름제어<br/>
> 수신자와 송신자의 메시지 처리속도 차이를 해결하기 위한 방법<br/>
수신자는 윈도우 크기를 자신의 응답 헤더에 담아서 송신 측에게 전해주게 되고, 송신자는 상대방에게 데이터를 보낼 때 이 윈도우 크기를 확인

> TCP 오류제어<br/> 
> 수신자와 송신자의 패킷 오류 처리를 하는 방법<br/>
수신자가 송신자에게 명시적으로 NACK(부정응답)을 보내거나 송신자에게 ACK(긍정응답)가 오지 않거나 중복된 ACK가 계속 해서 오면 오류가 발생했다고 판단

> TCP 혼잡제어<br/>
> 송신자와 네트워크(라우터)의 데이터 처리 속도 차이를 해결하기 위한 방법 <br/>
> 패킷 손실 시 파악되는 타임 아웃이나 중복된 ACK을 통해서 혼잡을 파악 <br/>
ACK을 확인하지 않고도 보낼 수 있는 데이터 양인 CWND(Congestion Window)를 기반으로 동작

> UDP는 신뢰성을 보장하지 않지만 추가적인 정의를 통해 보장 가능<br/>
> HTTP/3에서 QUIC 프로토콜

<br/>

### 3-way handshake와 4-way handshake
<div style="display: flex; flex-direction: row;">
  <img src="https://velog.velcdn.com/images%2Fnnnyeong%2Fpost%2F9943de2b-96d8-4e63-b9cc-46c1a89e20a3%2Fimage.png" alt="3handshake" width="50%">
  <img src="https://velog.velcdn.com/images%2Fnnnyeong%2Fpost%2Ffd5029e1-b84c-4fa3-9f7b-d5f702f1b1b9%2Fimage.png" alt="4handshake" width="50%">
</div>

- 3 way-handshake
    - TCP 네트워크에서 통신 하는 장치가 서로 연결이 잘 되었는지 확인하는 방법
- 4-way handshake
    - TCP 네트워크에서 통신 하는 장치의 연결을 해제하는 방법
    - TIME-WAIT: 아직 서버에서 받지 못한 데이터가 연결이 해제되어 유실되는 경우를 대비해 일정시간 잉여 패킷을 기다림

<br/>

### 쿠키와 세션 차이
- 쿠키
    - 사용자의 컴퓨터에 저장하는 데이터 파일
    - 예: 팝업창을 통해 "오늘 이 창을 다시 보지 않기" 체크
- 세션
    - 사용자(브라우저)로부터 들어오는 일련의 요구를 하나의 상태로 보고, 그 상태를 유지시키는 기술
    - 예: 화면을 이동해도 로그인이 풀리지 않고 로그아웃하기 전까지 유지

||쿠키|세션|
|-|-|-|
|저장 위치|Client PC|Web Server|
|라이프 사이클|쿠키 저장시 설정(브라우저가 종료되어도 인증이 유지)|브라우저 종료시 삭제|
|속도|빠름|느림(서버 처리 시간 소요)|
|보안|낮음(당사자가 아닌 제 3자도 조회 가능)|높음|

### 세션 기반 인증과 토큰 기반 인증
<img src="https://mblogthumb-phinf.pstatic.net/MjAxOTA1MjVfMTEg/MDAxNTU4Nzk0NTk1MDE5.lvPae_6FL3CLDXMcuuXNugZujgASiTx3b5uSUwnzPggg.TdBCmFZLyjIbn1u3xLlnL0OLGIT9noPjTGWG0lVsnLog.PNG.shino1025/994BEA345B53368401.png?type=w800" alt="session" width="100%">

- 세션 기반 인증: 클라이언트로부터 요청을 받으면 해당 상태 정보를 저장하므로 Stateful한 구조
    - 중요한 정보는 서버에 있기 때문에 세션 ID 쿠키에는 유의미한 값을 가지고 있지 않음
    - 서버에 세션을 저장하기 때문에 사용자가 증가하면 서버에 과부하
    - 분산 서버 활용 시, 상태 유지가 올바르게 작동하지 않을 수 있음
    - 세션 하이재킹: 훔친 세션 ID 쿠키를 이용해 요청을 보내면 서버는 올바른 사용자가 보낸 요청인지 알 수 없음
    - 예: 넷플릭스 디바이스 로그인 개수 제한

<img src="https://mblogthumb-phinf.pstatic.net/MjAxOTA1MjVfNDMg/MDAxNTU4Nzk1NjQ3Nzg5.cz-5fOL_RPyifrETlD_Go9cuUmyCl8Jrl01uY_T5PgUg.FE9xhe58eOPiC_ZUucbewNUHAf35kj9cjo3qStzO5msg.PNG.shino1025/asdasd.png?type=w800
" alt="session" width="100%">

- 토큰 기반 인증: Access Token을 발급해준 후 요청이 들어오면 검증만 해주면 되기 때문에 추가 저장소가 필요 없는 Stateless한 구조
    - 이미 발급된 토큰을 돌이킬 수 없으므로 유출 시, 토큰 만료전까지 피해가 계속 발생할 수 있음
    - (JWT에서의 대안) Refresh Token을 추가적으로 발급해서 Access 토큰의 사용기간을 단축

### JWT 토큰
- 웹에서 사용되는 인증에 필요한 정보를 암호화시킨 JSON 형식의 토큰
- JWT(JSON Web Token)의 구조
    - Header: 토큰의 타입과 Signature를 해싱하기 위한 암호화 알고리즘으로 구성
    - Payload: 토큰에 서비스에서 사용자에게 토큰을 통해 공개하기를 원하는 내용(= Claim), JSON(Key/Value) 형태
    - Signature: 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드

<br/>

### 암호화 방식
- 단방향 암호화 방식: 복호화 불가능
    - 예시: 사용자 비밀번호
- 양방향 암호화 방식: 복호화 가능
    - 대칭키: 암호화와 복호화에 같은 키를 사용
        - 빠른 속도, 키 노출 위험
    - 비대칭키: 암호화와 복호화할 때 키를 서로 다른 키로 사용
        - 느린 속도(메시지 암호화에는 쓰이지 않고 주로 키를 암호화하는데에 사용), 높은 안정성
        - 예시: 공인인증서

<br/>

### OSI 7 Layer Model
1. 물리 계층(Physical Layer)
    - 0과 1의 비트 정보를 회선에 보내기 위한 전기적 신호 변환
2. 데이터 링크 계층(Data Link Layer)
    - <b>인접</b> 시스템 간 데이터 전송, 전송 오류 제어를 통한 신뢰성 구축
3. 네트워크 계층(Network Layer)
    - 단말기 간 데이터 전송을 위한 최적화된 경로 제공
    - Protocol: IP
4. 전송 계층(Transport Layer)
    - <b>송수신 프로세스(종단)</b> 간의 연결. 신뢰성 있는 통신 보장
    - Protocol: TCP, UDP
5. 세션 계층(Session Layer)
    - 송수신 간의 논리적 연결
6. 표현 계층(Presentation Layer)
    - 데이터 형식 설정, 암/복호화
7. 응용 계층(Application Layer)
    - 일반적인 응용 서비스를 수행

<br/>

### 로드 밸런싱
#
로드 밸런서를 클라이언트와 서버 사이에 두고, 부하가 집중되지 않도록 여러 서버에 분산하는 방식
- Scale out(서버를 여러 대 추가하여 시스템을 확장하는 방식) 시에 사용
- Server Load Balancing이라고도 불림

로드 밸런서의 역할
- NAT(Network Address Translation): 사설IP - 공인IP 전환
- Tunneling: 데이터를 캡슐화하여 연결된 노드만 캡슐을 해제할 수 있게 만듦
- DSR(동적 소스 라우팅): 요청에 대한 응답을 할 때 로드밸런서가 아닌 클라이언트의 IP로 응답

L4 로드 밸런싱
- IP와 PORT 기반의 로드 밸런싱
- 보통 L4 스위치 장비로 로드밸런싱하며 가격이 비쌈
- VIP*를 통한 로드 밸런싱은 L4 로드밸런싱
  
L7 로드 밸런싱
- URI, Payload, Http Header, Cookie 등 기반의 로드 밸런싱
- 보통 L7 스위치 장비로 로드밸런싱하며 가격이 비쌈
- nginx나 apache를 통한 로드 밸런싱은 L7 로드밸런싱

> \* VIP(Virtual IP)
> 
> 여러 개의 실제 서버를 대표하는 가상의 IP로 DNS와 VIP를 연결하여 다수의 서버에 연결할 때 사용<br/>
VIP는 IP 기반의 로드 밸런싱하는 역할을 겸할 수 있음

<br>

### CORS(Cross Origin Resource Sharing)
#
CORS
- '교차 출처 리소스 공유'
- HTTP 헤더를 사용하여 한 출처(*Origin)에서 실행중인 웹 어플리케이션이 다른 출처(cross-origin)의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 정책

> \* Origin : Protocol + Host + Port

CORS 해결 in SpringBoot
1. javax.servlet.Filters 사용하여 필터링하기
2. @CrossOrigin 어노테이션 사용 (클래스, 메서드 단위 설정)
3. WebMvcConfigurer에서 설정 (Bean 등록)

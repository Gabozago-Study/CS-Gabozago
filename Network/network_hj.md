# Network

### HTTP(Hyper Text Transfer Protocol)
- 데이터를 주고 받기 위한 프로토콜
- 상태 정보를 저장하지 않는 Stateless 및 라이언트의 요청에 맞는 응답을 보낸 후 연결을 끊는 Connectionless 특징
    - 연결 상태 처리나 상태 정보를 관리할 필요가 없어 서버 디자인이 간단
    - 통신의 정보를 모르기 때문에 매번 인증 필요 
        - 해결방안: 쿠키, 세션 등

### HTTP Method
|종류|기능|
|-|-|
|GET|데이터 조회|
|POST|요청 데이터 처리, 주로 등록에 사용|
|PUT|리소스를 대체(덮어쓰기), 해당 리소스가 없으면 생성|
|PATCH|리소스 부분 변경 (PUT이 전체 변경, PATCH는 일부 변경)|
|DELETE|데이터 삭제|

### HTTP 상태 코드
- 1xx : 정보 응답
- 2xx : 성공 응답
- 3xx : 리다이렉트, 요청을 완료하려면 추가적인 작업(페이지 이동)이 필요
- 4xx : 클라이언트 요청 오류
- 5xx : 서버 오류

### HTTP와 HTTPS의 차이점
- HTTP
    - 평문 데이터를 전송하는 프로토콜
    - TCP와 직접 통신
- HTTPS
    - HTTP에 암호화가 추가된 프로토콜
    - HTTP는 SSL과 통신 + SSL이 TCP와 통신

### TCP와 UDP의 차이
||TCP|UDP|
|-|-|-|
|연결 방식|연결형(3-way handshake)|비 연결형|
|전송 순서|보장|보장 X|
|수신 여부 확인|O|X|
|속도|느림|빠름|
|신뢰성|높음|낮음|

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

### 쿠키와 세션 차이
- 쿠키
    - 사용자의 컴퓨터에 저장하는 작은 기록 정보 파일
    - 예: 팝업창을 통해 "오늘 이 창을 다시 보지 않기" 체크
- 세션
    - 일정 시간 동안 같은 사용자(브라우저)로부터 들어오는 일련의 요구를 하나의 상태로 보고, 그 상태를 유지시키는 기술
    - 웹 서버의 저장되는 쿠키(=세션 쿠키)
    - 예: 화면을 이동해도 로그인이 풀리지 않고 로그아웃하기 전까지 유지

||쿠키|세션|
|-|-|-|
|저장 위치|Client PC|Web Server|
|라이프 사이클|쿠키 저장시 설정(브라우저가 종료되어도 인증이 유지)|브라우저 종료시 삭제|
|속도|빠름|느림|
|보안|낮음(당사자가 아닌 제 3자도 조회 가능)|높음|

### 세션 기반 인증과 토큰 기반 인증
<img src="https://mblogthumb-phinf.pstatic.net/MjAxOTA1MjVfMTEg/MDAxNTU4Nzk0NTk1MDE5.lvPae_6FL3CLDXMcuuXNugZujgASiTx3b5uSUwnzPggg.TdBCmFZLyjIbn1u3xLlnL0OLGIT9noPjTGWG0lVsnLog.PNG.shino1025/994BEA345B53368401.png?type=w800" alt="session" width="100%">

- 세션 기반 인증: 클라이언트로부터 요청을 받으면 해당 상태 정보를 저장하므로 Stateful한 구조
    - 중요한 정보는 서버에 있기 때문에 세션 ID(쿠키)에는 유의미한 값을 가지고 있지 않음
    - 서버에 세션을 저장하기 때문에 사용자가 증가하면 서버에 과부하
    - 세션 하이재킹: 훔친 쿠키를 이용해 요청을 보내면 서버는 올바른 사용자가 보낸 요청인지 알 수 없음

<img src="https://mblogthumb-phinf.pstatic.net/MjAxOTA1MjVfNDMg/MDAxNTU4Nzk1NjQ3Nzg5.cz-5fOL_RPyifrETlD_Go9cuUmyCl8Jrl01uY_T5PgUg.FE9xhe58eOPiC_ZUucbewNUHAf35kj9cjo3qStzO5msg.PNG.shino1025/asdasd.png?type=w800
" alt="session" width="100%">

- 토큰 기반 인증: Access Token을 발급해준 후 요청이 들어오면 검증만 해주면 되기 때문에 추가 저장소가 필요 없는 Stateless한 구조
    - 이미 발급된 JWT를 돌이킬 수 없으므로 유출 시, 만료전까지 피해가 계속 발생할 수 있음

### JWT 토큰
- 웹에서 사용되는 인증에 필요한 정보를 암호화시킨 JSON 형식의 토큰
- JWT(JSON Web Token)의 구조
    - Header: 토큰의 타입과 Signature를 해싱하기 위한 암호화 알고리즘으로 구성
    - Payload: 토큰에 사용자가 담고자 하는 정보를 담는 곳, JSON(Key/Value) 형태
    - Signature: 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드

### 암호화 방식
- 단방향 암호화 방식: 복호화 불가능
    - 예시: 사용자 비밀번호
- 양방향 암호화 방식: 복호화 가능
    - 대칭키: 암호화와 복호화에 같은 키를 사용
        - 빠른 속도, 키 노출 위험
    - 비대칭키: 암호화와 복호화할 때 키를 서로 다른 키로 사용
        - 느린 속도(메시지 암호화에는 쓰이지 않고 주로 키를 암호화하는데에 사용), 높은 안정성
        - 예시: 공인인증서

### 공인(public) IP와 사설(private) IP의 차이
- 공인 IP: ISP(인터넷 서비스 공급자)가 제공하는 IP 주소
- 사설 IP
    - 일반 가정이나 회사 내 등에 할당된 네트워크 IP 주소
    - IPv4의 주소부족으로 인해 서브넷팅된 IP이기 때문에 라우터(공유기)에 의해 로컬 네트워크상의 PC나 장치에 할당
- 사설 IP 주소만으로는 인터넷에 직접 연결할 수 없고, 라우터를 통해 1개의 공인 IP를 할당하고, 라우터에 연결된 개인 PC는 사설 IP를 각각 할당 받아 인터넷에 접속

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

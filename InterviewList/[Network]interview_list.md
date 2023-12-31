# [Network] Interview List

### [Q] HTTP 특징?
#
상태 정보를 저장하지 않는 <b>Stateless</b> 및 클라이언트의 요청에 맞는 응답을 보낸 후 연결을 끊는 <b>Connectionless</b> 특징을 갖습니다. <br/>
연결 상태 처리나 상태 정보를 관리할 필요가 없어 서버 디자인이 간단하지만, 상태 유지가 되지 않으므로 매번 인증 필요한 단점이 있습니다.

<br>

### [Q] GET 메서드와 POST 메서드 차이?
#
GET 메서드는 URL에 요청 정보를 붙여서 데이터 조회하므로 POST 방식보다 보안상 취약합니다. 그러나, 캐싱을 사용할 수 있어 POST 방식보다 빠르다는 장점이 있습니다. <br/>
POST 메서드는 요청 정보를 HTTP 패킷의 Body 안에 숨겨서 서버로 전송하여 데이터를 등록하므로 GET 방식보다 보안상 안전합니다.

<br>

### [Q] RESTful API란?
#
REST 기반으로 서비스 API를 구현하는 것입니다. <br/>
REST는 URI로 자원을 명시하며, HTTP METHOD를 통해 자원에 대한 행위를 표현하는 것을 의미합니다. <br/>
예를 들어, "GET/members/1"을 통해 RESTful API를 구현할 수 있습니다.

<br>

### [Q] HTTPS의 장단점
#
HTTP에 SSL 또는 TLS를 통해 데이터를 암호화할 경우, 안전하다는 장점이 있습니다. <br/>
그러나, 암호화 과정에서 웹 서버에 부하가 생길 수 있으며, 속도가 지연되고 추가 비용이 발생할 수 있습니다.

<br>

### [Q] TCP, UDP 차이
#
TCP는 연결형 프로토콜로, 전송 순서와 온전한 데이터 송수신이 보장되어 신뢰성이 높습니다. <br/>
그러나 연결과정에서 시간이 소요되므로 속도가 중요한 서비스인 스트리밍에서는 UDP 프로토콜이 사용됩니다.

<br>

### [Q] TCP에서 제공하는 제어기능 종류
#
수신자와 송신자의 메시지 처리속도 차이를 해결하기 위한 <b>흐름제어</b>, 수신자와 송신자의 패킷 오류 처리를 하는 <b>오류 제어</b>, 송신자와 네트워크(라우터)의 데이터 처리 속도 차이를 해결하기 위한 <b>혼잡 제어</b>가 있습니다.

<br>

### [Q] 쿠키와 세션의 차이
#
쿠키는 Client PC에 저장되며, 유효 기간을 따로 설정할 수 있어 브라우저가 종료되어도 유지될 수 있습니다. Client PC에 저장되어있어 속도는 빠르지만, 데이터 노출과 조작 위험에 취약하여 보안성은 세션에 비해 낮습니다. <br/>
이와 달리 세션은 웹 서버에 저장되므로 쿠키보다 안전하지만, 속도는 상대적으로 느립니다. 또한 웹 서버에 저장되므로 브라우저가 종료될 경우, 세션은 삭제됩니다.

### [Q] 세션 기반 인증
#
사용자의 인증 정보가 서버의 세션 저장소에 저장되는 방식으로 사용자가 증가하면 서버에 부담이 될 수 있습니다. 또한, 분산 서버 활용 시, 상태 유지가 올바르게 작동하지 않을 수 있는 위험이 있습니다. <br/>
그러나, 관리자가 세션을 관리할 수 있는 장점이 있으므로 '디바이스 로그인 개수 제한' 등에 활용할 수 있습니다.

<br>

### [Q] Token 기반 인증
#
인증받은 사용자에게 토큰을 발급해주고, 서버에 요청을 할 때마다 HTTP 헤더에 토큰을 함께 보내서 인증된 사용자가 맞는지 확인하는 방식입니다. <br/>
그러나, 토큰의 경우에도 이미 발급된 토큰을 무효화 할 수 없으므로 유출 시, 토큰 만료전까지 피해가 계속 발생할 수있다는 단점이 있습니다. JWT에서는 이러한 단점을 보안하기 위해 Refresh Token를 활용하여 Access Token 유출에 대비하고 있습니다.

<br>

### [Q] JWT를 활용하여 로그아웃을 구현하는 방법
#
클라이언트가 갖고 있는 토큰은 서버에서 삭제할 수 없습니다. 그러므로 로그아웃 시, Access Token을 redis같은 캐시 서버에 저장을 해두고 요청이 왔을 때, redis에 해당 access token이 존재하는지 확인하여 만료된 토큰인지 식별하는 방법으로 로그아웃을 구현할 수 있습니다.

<br>

### [Q] 트래픽 증가에 따른 서버 확장 방법
#
서버의 하드웨어 성능을 업그레이드하는 Scale-up과 비슷한 성능의 서버를 여러대 증설하는 Scale-out이 있습니다. <br/>
스케일 아웃을 사용할 경우, 각 서버에 트래픽을 알맞게 나눠줘야하기 때문에 로드 밸런서가 필요합니다.

<br>

### [Q] 로드 밸런서의 역할
#
트래픽을 균등하게 분산시켜줄 뿐만 아니라, 하나의 서버에 장애가 발생해도 다른 서버로 트래픽을 전달하여 서비스의 지속성을 보장합니다. 또한 동일한 클라이언트의 요청이 항상 같은 서버로 전달되도록 하여, 세션 정보 교환에 따른 서버의 부하를 줄여줍니다.

<br>

### [Q] 로드 밸런싱 종류
#
MAC주소를 바탕으로 로드 밸런싱하는 L2, IP주소를 바탕으로 로드 밸런싱 L3, TCP/UDP가 속한 전송계층 단계에서 로드 밸런싱하는 L4, HTTP/HTTPS가 속한 응용계층 단계에서 로드 밸런싱하는 L7이 있습니다.

<br>

### [Q] CORS(Cross Origin Resource Sharing)란?
#
HTTP 헤더를 사용하여, 하나의 출처에서 실행중인 웹 어플리케이션이 다른 출처(cross-origin)의 자원에 접근할 수 있는 권한을 부여하기 위한 정책을 의미합니다.
서버는 응답 헤더에 특정 출처에서 오는 요청을 허용하는 설정을 포함시킴으로써 클라이언트가 해당 리소스에 접근하도록 할 수 있습니다.
SpringBoot에서는 CORS를 해결하기 위해 필터링, @CrossOrigin, WebMvcConfigurer를 활용할 수 있습니다.
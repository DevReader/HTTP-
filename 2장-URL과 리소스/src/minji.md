# URL과 리소스
## 인터넷의 리소스 탐색하기
* URI 는 HTTP 프로토콜이 아닌 다른 가용한 프로토콜 사용 가능
  * `mailto:~` : 이메일 주소
  * `ftp://~` : FTP(File Transfer Protocol) 서버에 올라가 있는 파일
  * `rtsp://~`
* 대부분의 URL 은 `스킴://서버위치/경로` 구조로 이루어짐

### URL 이 있기 전 암흑의 시대
* URL이 있기 전엔 애플리케이션마다 다르게 갖고 있는 분류 방식 사용했었음
* URL은 브라우저가 더 영리하게 리소스에 접근하고 다루게 함으로써 온라인 세상을 단순화 함
<br/><br/>

## URL 문법
* URL 문법은 스킴에 따라 달라짐. 하지만 대부분의 URL 은 일반 URL 문법을 따라 문법면에서 매우 유사
* <스킴>://<사용자이름>:<비밀번호>@<호스트>:<포트>/<경로>;<파라미터>?<질의>#<프래그먼트>

### 스킴: 사용할 프로토콜
* 주어진 리소스에 어떤 프로토콜을 사용해 접근해야하는지 알려줌
* 알파벳으로 시작해야 하고 `:` 문자로 구분함
* 대소문자 구분하지 않음

### 호스트와 포트
* 호스트 컴포넌트 - 리소스를 보유한 인터넷 상의 호스트 장비를 가리킴
* 포트 컴포넌트 - 서버가 열어놓은 네트워크 포트(TCP 프로토콜 사용한다면 기본 포트는 80)

### 사용자 이름과 비밀번호
* 사용자 이름과 비밀번호가 없는 경우 이름은 `anonymous`, 빔리번호는 브라우저 기본값을 사용(크롬의 경우 chrome@example.com)

### 경로
* 리소스가 서버의 어디에 있는지 알려줌
* 유닉스 파일 시스템의 파일 경로와 유사함

### 파라미터
* 서버에 명확한 요청을 하기 위해 필요한 입력 파라미터를 받는데 사용
* 이름/값 쌍의 리스트로 URL 나머지 부분들로부터 `;` 문자로 구분해 URL 에 기술
* ex) http://www.devtato.com/index.html;graphics=true

### 질의 문자열
* 리소스 형식의 범위를 좁히기 위한 질문/질의
* ex)http://www.devtato.com/index.html;id=123
* 사용하며 안 되는 특정 문자열을 제외하고는 질의 컴포넌트 포맷 제약사항은 없지만, 편의상 게이트웨이가 `&` 으로 나뉜 `이름=값` 쌍 형식의 질의 문자열을 사용

### 프래그먼트
* 리소스의 특정 부분/ 조각을 가리킴
* URL 의 오른쪽에 `#` 문자에 이어서 옴
* ex)http://www.devtato.com/index.html#drills
* 서버에서는 리소스 전체만 다루기 때문에 서버에 전달하지 않고, 전체 리소스를 내려 받은 후 일부만 보여주는 방식
<br/><br/>

## 단축 URL
### 상대 URL
* URL은 상대 URL 과 절대 URL 두 가지로 나뉨
* 절대 URL - 모든 정보 담음
* 상대 URL - 모든 정보 담지 않음. 기저(base) URL 필요. 프래그먼트 이거나 URL 의 일부임
* URL 을 처리하는 애플리케이션에서는 상대 URL 과 절대 URL 간 상호 변환 가능해야 함

### URL 확장
* URL 을 빠르게 입력할 수 있도록 부분만 입력하면 전체로 확장해줌
* 호스트명 확장
  * 단순한 휴리스틱 사용으로 호스트명을 전체 호스트명으로 확장
  * 프락시와 같은 HTTP 애플리케이션에 문제 일으킬 수 있음
* 히스토리 확장
  * 과거에 사용자가 방문했던 URL의 기록을 저장해 놓고 완결 형태 선택하게 해줌
  * 프락시를 사용할 경우 다르게 동작할 수 있음
<br/><br/>

## 안전하지 않은 문자
* 모든 프로토콜이 데이터 전송을 위해 서로 다른 장치를 가지고 있기 때문에 어떤 인터넷 프로토콜을 통해서도 안전하게 전송될 수 있도록 URL 설계하는 것이 중요
* SMTP(Simple Mail Transfer Protocol)
  * 전자메일에 사용되는 프로토콜로 특정 문자를 제거할 수도 있는 전송 방식 사용
  * 문자가 제거되는 일을 피하기 위해 상대적으로 작고 일반적으로 안전한 알파벳 문자만 포함하도록 허용 함

### URL 문자 집합
* 많은 컴퓨터 애플리케이션이 US-ASCII 문자 집합 사용해 왔음
* US-ASCII: 7비트를 사용해 영문 자판 키 대부분과 출력되지 않는 제어 문자 표현
  * 적은 수의 문자만을 포함하고 있음
  * 이진 데이터를 포함하는 URL의 경우 이스케이프 문자열이 필요한데 US-ASCII 에선 사용이 금지되어 있음

### 인코딩 체계
* 안전하지 않은 문자를 `%` + 두 개의 16진수 숫자로 이루어진 이스케이프 문자로 변경

### 문자 제한
* URL 에서 예약된 문자를 본래의 목적이 아닌 다른 용도로 사용하려면 반드시 인코딩 해야하는 문자들이 있음 -> %, /, ., .., #, ?, ;, : 등

### 좀 더 알아보기
* 안전하지 않은 문자를 URL 에 사용해도 문제가 없을 수 있지만, 애플리케이션은 정해진 방식대로 구현해야 하므로 어떤 애플케이션에 어떤 URL 을 보내든, 안전하지 않거나 제한된 문자는 변환하는 것이 좋음
* 최초로 URL 을 입력받는 애플리케이션에서 어떤 문자를 인코딩할 지 결정하는 것이 적절함
  * URL 구성 컴포넌트 별 사용 가능한 문자가 다름
  * 어떤 문자는 스킴에 따라 가용성이 달라질 수 있음
  => 최초로 입력받는 곳이 가장 적절함
* 극단적으로는 모든 문자를 인코딩하는 방법이 있음
  * 안전한 것도 재차 인코딩 하기 때문에 빠르고 완벽함
  * 안전한 문자들을 인코딩하지 않는 애플리케이션도 있기 때문에 오동작 일으킬 수 있음
* 스킴 같은 몇몇 URL 컴포넌트는 쉽게 알아볼 수 있고 알파벳 문자로 시작해야 함
<br/><br/>

## 스킴의 바다
* http, https, mailto, ftp, rtsp, rtspu, file, news, telnet 등이 있음
<br/><br/>

## 미래
* URL은 리소스의 **주소**지 **이름**이 아님 -> 리소스가 옮겨지면 URL을 더이상 사용할 수 없음
* 객체가 옮겨지더라도 항상 객체를 가리킬 수 있는 이름인 URN 등장
* 지속 통합 자원 지시자(Persistent Uniform Resource Locators, PURL)을 사용하면 URL 로 URN 의 기능을 제공할 수 있음
  * 실제 URL 목록을 관리하고 추적하는 리소스 위치 중개 서버를 두고 리소스를 우회적으로 제공
  * 클라이언트가 위치 할당자에게 리소스를 가져올 수 있는 영구 URL 을 요청하면 영구적인 URL은 클라이언트를 리소스의 실제 URL 로 연결해줌

### 지금이 아니면, 언제?
* URN이 채택되지 않은 이유는 URN 지원을 위해서 해야할 작업이 많고 URL은 한계를 가지고 있지만 긴급한 사안이 아니기 때문


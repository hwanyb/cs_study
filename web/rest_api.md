# 📌 REST API
## ✅ REST 란 무엇인가요?
- **"REpresentational State Transfer"** 의 약자로
자원을 이름(자원의 표현)으로 구분해 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미합니다.
- 즉, 자원(resource)의 표현(representation)에 의한 상태 전달을 뜻합니다.
    1. 자원 : 해당 SW가 관리하는 모든 것 (문서, 그림, 데이터 등)
    2. 표현 : 그 자원을 표현하기 위한 이름 (학생 정보가 자원이라면 'students' 등)
    3. 상태 전달 : 데이터가 요청되는 시점에 자원의 상태를 전달 (JSON 혹은 XML)
- 어떤 자원에 대해 CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해
URI(Resource)로 GET, POST 등의 방식(Method)을 사용하여 요청을 보내며, 요청을 위한 자원은 특정한 형태(Representation of Resource)로 표현

        URI 와 URI의 차이점
        - URI : Uniform Resource Locator로 인터넷 상 자원의 위치
        - URL : Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성(URI는 URL을 포함함)

## ✅ REST의 구성요소는 무엇인가요?
1. 자원(Resource) - `URI`
    - 모든 자원에는 고유한 ID가 존재하고, 이 자원은 Server에 존재함
    - 자원을 구별하는 ID는 `'/exgroups/:exgroup_id'`와 같은 HTTP URI 임
    - Client는 URI를 이용해 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청
2. 행위(Verb) - `Method`
    - HTTP 프로토콜의 Method(`GET`, `POST`, `PUT`, `PATCH`, `DELETE`)를 사용
    - `GET` : Read, 정보 요청, URI가 가진 정보를 검색하기 위해 요청
    - `POST` : Create, 정보 입력, 클라이언트가 서버로 정보를 전달
    - `PUT` : Update, 정보 업데이트, 데이터 전체를 바꿀때
    - `PATCH` : Update, 정보 업데이트, 데이터 일부를 바꿀때
    - `DELETE` : Delete, 정보 삭제, 안정성 문제로 서버에서 대부분 비활성화함
3. 표현(Representation of Resource)
    - Client와 Server가 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등이 있음
    - JSON, XML을 통해 데이터를 주고 받는 것이 일반적
## ✅ REST의 특징은 무엇인가요?
1. Server-Client (서버-클라이언트 구조)<br />
    : 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client
2. Stateless (무상태)<br />
    : HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성
3. Cacheable (캐시 처리 기능)
4. Layered System (계층 구조)
5. Uniform Interface (인터페이스 일관성)
6. Self-Descriptiveness (자체 표현)

## ✅ REST API가 무엇인가요?
REST의 특징을 기반으로 서비스 API를 구현한 것입니다.
- REST API 디자인 가이드
    - URI는 정보의 자원을 표현해야 합니다. <br />
    ex) `/user`, `/review` 등
    - 자원에 대한 행위는 HTTP Method(GET, POST 등)로 표현합니다. (행위는 URL에 포함하지 않습니다.)
- REST API 설계규칙
    1. URI는 명사를 사용합니다<br />
        - `/getUsers`, `/createNewUser` (❌)
        - `/user`, `/review` (⭕)
    2. 슬래시(/)로 계층관계를 표현합니다
        - `/review/comment`
    3. URI 마지막 문자로 슬래시( / )를 포함하지 않습니다.
    4. 밑줄( _ )을 사용하지 말고 하이픈( - )을 사용합니다.
    5. URI는 소문자로만 구성합니다.
    6. HTTP 응답 상태 코드 사용합니다.
        - 클라이언트는 해당 요청에 대한 실패 처리완료, 잘못된 요청 등에 대한 피드백 필요합니다.
        - 2xx은 성공 / 4xx은 클라이언트 실패 / 5xx은 서버 실패를 의미합니다.
    7. 파일확장자는 URI에 포함하지 않습니다.

## ✅ REST API 와 RESTful API의 차이점이 무엇인가요?
    RESTful은 REST의 설계 규칙을 잘 지켜서 설계된 API를 RESTful한 API라고 합니다.
    즉, REST의 원리를 잘 따르는 시스템을 RESTful이란 용어로 지칭합니다.
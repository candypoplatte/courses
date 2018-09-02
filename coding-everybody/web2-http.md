# Web2. HTTP

## HTTP?

- HyperText Transfer Protocol
- Web 상에서 정보를 주고 받는 규약
- Server 와 Client 사이의 Request와 Response 규약
- [WorldWideWeb: Proposal for a HyperText Project](https://www.w3.org/Proposal.html)

## Request

- Client -> Server

### Request Message

- 요청 시 보내는 Message
- 구성
  - **Request Line**
    - 시작 줄
    - `Request Method`  `Request Target`  `HTTP Version`
    - ex) `GET`  `example.com`  `HTTP/1.1`
    - [HTTP request methods - HTTP | MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)
  - **Request Headers**
    - Request를 부연 설명하는 내용
    - [List of HTTP header fields - Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
    - `Header 명`:  `Header 값`
    - 주요 Header 
      - Host : host정보 (서버의 도메인 이름 & 포트)
      - User-Agent : Web Browser 정보 
        - 사용자를 대신해서 일(웹 접속)을 하는 SW = Web Browser
        - [User agent - Wikipedia](https://en.wikipedia.org/wiki/User_agent#User_agent_identification)
      - Accept-Encoding : Browser가 읽을 수 있는(Decoding 가능한) Encoding 종류를 알려줌
      - If-Modified-Since
  - *Header와 Body 사이에는 1줄 띄움*
  - **Request Message Body**  
    - Header와 Body 사이에는 1줄 띄움
    - 서버쪽으로 전송할 내용

## Response

- Server -> Client

### Response Message

- 응답 시 보내는 Message
- 구성
  - **Status Line**
    - 시작 줄
    - `Version`  `Status Code`  `Phrase`
    - ex) `HTTP/1.1`  `404`  `Not Found`
    - [List of HTTP status codes - Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
  - **Response Headers**
    - Response를 부연 설명하는 내용
    - [List of HTTP header fields - Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
    - `Header 명`:  `Header 값`
    - 주요 Header 
      - Content-Type : Content의 MIME type(media type)
        - [Media type - Wikipedia](https://en.wikipedia.org/wiki/Media_type)
      - Content-Length
      - Content-Encoding : Data를 Encoding한 방식
      - Last Modified
  - *Header와 Body 사이에는 1줄 띄움*
  - **Response Message Body**  
    - Header와 Body 사이에는 1줄 띄움
    - 본문

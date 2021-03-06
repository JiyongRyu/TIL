# 38. 브라우저의 렌더링 과정

- 파싱(parsing)

  파싱(구문 분석, syntax analysis)은 프로그래밍 언어의 문법에 맞게 작성된 텍스트 문서를 읽어 들여 실행하기 위해 텍스트 문서의 문자열을 토큰으로 분해하고, 토큰에 문법적 의미와 구조를 반영하여 트리 구조의 자료 구조인 파스 트리를 생성하는 일련의 과정을 말한다.

- 렌더링(rendering) 

  HTML, CSS, 자바스크립트로 작성된 문서를 파싱하여 브라우저에 시각적으로 출력하는 것을 말한다.

- 브라우저 렌더링 실행 과정

  1. 브라우저는 HTML, CSS, 자바스크립트, 이미지, 폰트 파일 등의 렌더링에 필요한 리소스를 요청하고 서버로부터 응답을 받는다.
  2. 브라우저의 렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱하여 DOM과 CSSOM을 생성하고 이들을 결합하여 렌더 트리를 생성한다.
  3. 브라우저의 자바스크립트 엔진은 서버로부터 응답된 자바스크립트를 파싱하여 AST(Abstract Syntax Tree)를 생성하고 바이트 코드로 변환하여 실행한다. 이때 자바스크립트는 DOM API를 통해 DOM, CSSOM을 변경할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합된다.
  4. 렌더 트리를 기반으로 HTML 요소의 레이아웃(위치와 크기)를 계산하고 브라우저의 화면에 HTML 요소를 페인팅한다.

### 1. 요청과 응답

- 브라우저의 핵심 기능은 필요한 리소스(HTML, CSS, 자바스크립트, 이미지, 폰트 등의 정적 파일 또는 서버가 동적으로 생성한 데이터)를 서버에 요청(request)하고 서버의 응답(response)을 받아 브라우저에 시각적으로 렌더링하는 것이다. 
- 서버에 요청을 하기 위해 브라우저는 주소창을 제공한다. 브라우저의 주소창에 URL을 입력하고 엔터 키를 입력하면 URL의 [호스트 이름](https://ko.wikipedia.org/wiki/호스트명)은 [DNS](https://ko.wikipedia.org/wiki/도메인_네임_시스템)를 통해 IP 주소로 변환되고 이 IP 주소를 갖는 서버에게 요청(request)를 전송한다.

### 2. HTTP 1.1와 HTTP 2.0

- HTTP/1.1은 기본적으로 커넥션(connection) 당 하나의 요청과 응답 만을 처리한다. 
- HTTP/2는 커넥션 당 여러 개의 요청과 응답, 즉 다중 요청/응답이 가능하다.

### 3. HTML 파싱과 DOM 생성

- 브라우저의 요청에 의해 서버가 응답한 HTML 문서는 문자열로 이루어진 순수한 텍스트이다. 순수한 텍스트인 HTML 문서를 브라우저에 시각적인 픽셀로 렌더링하려면 HTML 문서를 브라우저가 이해할 수 있는 자료구조(객체)로 변환하여 메모리에 저장해야 한다.



![38-6](https://poiemaweb.com/assets/fs-images/38-6.png)

1. 서버에 존재하던 HTML 파일이 브라우저의 요청에 의해 응답된다. 이때 서버는 브라우저가 요청한 HTML 파일을 읽어 들여 메모리에 저장한 다음 메모리에 저장된 바이트(2진수)를 인터넷을 경유하여 응답한다.
2. 브라우저는 서버가 응답한 HTML 문서를 바이트(2진수) 형태로 응답 받는다. 그리고 바이트 형태의 HTML 문서는 meta 태그의 charset 어트리뷰트에 의해 지정된 인코딩 방식(예를 들어 UTF-8)을 기준으로 문자열로 변환된다.
3. 문자열로 변환된 HTML 문서를 읽어 들여 문법적 의미를 갖는 코드의 최소 단위인 토큰(token)들로 분해한다.
4. 각 토큰들을 객체로 변환하여 노드(node) 들을 생성한다. 토큰의 내용에 따라 문서 노드, 요소 노드, 어트리뷰트 노드, 텍스트 노드가 생성된다. 노드는 이후 DOM을 구성하는 기본 요소가 된다.
5. HTML 문서는 HTML 요소들의 집합으로 이루어지며 HTML 요소는 중첩 관계를 갖는다. 즉, HTML 요소의 컨텐츠 영역(시작 태그와 종료 태그 사이)에는 텍스트 뿐만 아니라 다른 HTML 요소도 포함될 수 있다. 이때 HTML 요소 간에는 중첩 관계에 의해 부자 관계가 형성된다. 이러한 HTML 요소 간의 부자 관계를 반영하여 모든 노드들을 트리 자료 구조로 구성한다. 이 노드들로 구성된 트리 자료 구조를 **DOM(Document Object Model)**이라 부른다.

### 4. CSS 파싱과 CSSOM 생성

- 렌더링 엔진은 DOM을 생성해 나가다가 CSS를 로드하는 link 태그나 style 태그를 만나면 DOM 생성을 일시 중단한다.

  그리고 link 태그의 href 어트리뷰트에 정의된 CSS 파일을 서버에 요청하여 로드한 CSS나 style 태그 내의 CSS를 HTML과 동일한 파싱 과정(바이트 → 문자 → 토큰 → 노드 → CSSOM)을 거치며 해석하여 **CSSOM(CSS Object Model)**을 생성한다. 이후 CSS 파싱을 완료하면 HTML 파싱이 중단된 지점부터 다시 HTML을 파싱하기 시작하여 DOM 생성을 재개한다.

### 5. 렌더 트리 생성

- 렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱하여 각각 DOM과 CSSOM를 생성한다. 그리고 DOM과 CSSOM은 렌더링을 위해 **렌더 트리(render tree)**로 결합된다.

![38-9](https://poiemaweb.com/assets/fs-images/38-9.png)

### 6. 자바스크립트 파싱과 실행

- CSS 파싱 과정과 마찬가지로 렌더링 엔진은 HTML을 한줄씩 순차적으로 파싱하며 DOM을 생성해 나가다가 자바스크립트 파일을 로드하는 script 태그나 자바스크립트 코드를 컨텐츠로 갖는 script 태그를 만나면 DOM 생성을 일시 중단한다.

  그리고 script 태그의 src 어트리뷰트에 정의된 자바스크립트 파일을 서버에 요청하여 로드한 자바스크립트 코드나 script 태그 내의 자바스크립트 코드의 파싱을 위해 자바스크립트 엔진에 제어권을 넘긴다. 이후 자바스크립트 파싱과 실행이 종료되면 렌더링 엔진으로 다시 제어권을 넘겨 HTML 파싱이 중단된 지점부터 다시 HTML 파싱을 시작하여 DOM 생성을 재개한다.

### 7. 리플로우와 리페인트

- 만약 자바스크립트 코드에 DOM이나 CSSOM을 변경하는 DOM API가 사용된 경우, DOM이나 CSSOM이 변경된다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합되고 변경된 렌더 트리를 기반으로 레이아웃과 페인트 과정을 거쳐 브라우저의 화면에 다시 렌더링한다. 이를 리플로우(reflow), 리페인트(repaint)라 한다.

![38-12](https://poiemaweb.com/assets/fs-images/38-12.png)

- 리플로우는 레이아웃 계산을 다시 하는 것을 말하며 노드 추가/삭제, 요소의 크기/위치 변경, 윈도우 리사이징 등 레이아웃에 영향을 주는 변경이 발생한 경우에 한하여 실행된다. 리페인트는 재결합된 렌더 트리를 기반으로 다시 페인트를 하는 것을 말한다.

### 8. 자바스크립트 파싱에 의한 HTML 파싱 중단

- 렌더링 엔진과 자바스크립트 엔진은 병렬적으로 파싱을 실행하지 않고 직렬적으로 파싱을 수행한다.

![38-13](https://poiemaweb.com/assets/fs-images/38-13.png)

### 9. script 태그의 async / defer 어트리뷰트

- 자바스크립트 파싱에 의한 DOM 생성이 중단(blocking)되는 문제를 근본적으로 해결하기 위해 HTML5부터 script 태그에 async와 defer 어트리뷰트가 추가되었다.

- async 어트리뷰트

  HTML 파싱과 외부 자바크립트 파일의 로드가 비동기적으로 동시에 진행된다. 단, 자바스크립트의 파싱과 실행은 자바스크립트 로드가 완료된 직후 진행되며 이때 HTML 파싱이 중단된다.

- defer 어트리뷰트

  HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다. 단, 자바스크립트의 파싱과 실행은 HTML 파싱이 완료된 직후, 즉 DOM 생성이 완료된 직후 진행된다. 따라서 DOM 생성이 완료된 이후(이때 DOMContentLoaded 이벤트가 발생한다.) 실행되어야 할 자바스크립트에 유용하다.
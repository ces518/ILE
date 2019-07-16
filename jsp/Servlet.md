# 서블릿

- 서블릿 (Servlet)
    - 자바 엔터프라이즈 에디션 웹 애플리케이션 개발용 스팩과 API를 제공한다.
    - 요청 단위당 쓰레드로 동작한다.
    - 핵심 클래스는 HttpServlet

- 서블릿 등장 이전에 사용하던 기술인 CGI(Common Gateway Interface)
    - 요청 단위당 프로세스를 생성.

- 장점
    - 빠르다.
    - 플랫폼에 독립적
    - 보안
    - 이식성
    - 컨텐츠와 비즈니스 로직을 분리할 수 있다.
    - 유지보수가 용이하다.
    - 기능 확장이 용이하다.

- 단점
    - 화면에 표현할 HTML코드를 프로그램적으로 작성해야한다.
    - 서비스 전 반드시 컴파일 되어야한다.
    - 이러한 단점을 보완하기위해 JSP가 개발됨.

- 서블릿 컨테이너
    - 서블릿을 동작시키기위한 실행 환경
    - TCP/IP 연결을 생성하고, HTTP프로토콜을 해석하는 과정을 수행
    - 종류
        - 톰캣
        - 제티
        - 언더토우
        - 등등..
    - 세션 관리
    - 네트워크 서비스
    - MIME기반 메시지 인코딩, 디코딩
    - 서블릿 라이프사이클 관리


- 라이프사이클
    - 1. 서블릿 컨테이너가 서블릿 인스턴스의 init() 메서드를 호출하여 초기화 (최초 1회실행)
    - 2. 서블릿 초기화 후 클라이언트의 요청을 수행할수 있으며, 각 요청은 별도의 스레드로 처리한다.
        - 모든 요청(GET, POST.. 등)에 service() 메서드가 호출됨
        - HTTP 요청을 받고 클라이언트로 응답을 보낸다.
        - HTTP Method에 따라 doGet, doPost 로 요청을 위임한다.
        - 일반적으로 doGet, doPost를 구현한다.
    - 3. 서블릿 컨테이너의 판단하에 서블릿인스턴스가 제거되는 시점에 destroy를 호출
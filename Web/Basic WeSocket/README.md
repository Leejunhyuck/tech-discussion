### 최근 회사에서 소켓통신을 통하여 동글모듈에 연결하여 작업을 하는데 새로운 창에서 소켓 커넥션이 연결되지 않는 현상이 있었다.

  1. 우선 처음 원인이 무엇인지 생각 해 보았는데, Javascript가 싱글스레드라서 소켓이 2개가 생성이 안되는게 아닐까 였습니다.
  2. 하지만 조금 생각 해 보면 싱글스레드라서 소켓이 2개가 생성되지 않는다면, 단일 컨텍스트로 1개도 생성이 되지 않아야 하는게 아닐까라고 생각이 이어지고(아래 그림 참조)
  3. 그래서 WebSocket에 대해서 조금 정리를 봐야겠다는 생각이 들어 정리합니다.
  4. PS 원인은 연결하는 모듈에서 2개의 커넥션연결이 되지 않아서 였습니다..

    * 웹소켓 주소는 ws나 wss로 시작하는데 ws는 일반 웹소켓이고 wss는 SSL이적용된 웹소켓이다(Https)
    * websocket은 http와 같은 프로토콜로써 하나의 통신규약을 의미한다. 
        1. http 요청-응답 사용하여 연결을 설정한다. (Upgrade: Websocket, http 통신은 최초 1번)
        2. 서버와 TCP Connection을 유지하고 서로 통신한다 

    * 여기서 궁금한 점은 
      1. 어떻게 TCP Connection을 유지하느냐..
        * 

      2. 또한 어떻게 통신 및 메시지 송수신방법 하냐는 것인데.. 
        * 한번 연결한 connection은 유지하고, 보내고 받는 것을 이벤트 형식으로 받는다. 그러면 이벤트 형식으로 수신된다. 이 후 상황은 Javascript 비동기 처리방식 동작원리
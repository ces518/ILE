# ReadTimeout

#### 서론
- 요즈음에는 모놀리틱 아키텍쳐 보단 MSA 형태로 역할을 분리하여 구성을 한다.
- MSA란 하나의 서버에서 모든 역할을 수행하는것이 아닌, 각 역할별로 별도의 서버로 분리해 API 형태로 데이터를 제공하는 형태이다.
- 즉 MSA 환경에서 API 간의 통신이 중요해진다.

> API 응답속도, timeout 설정 등이 중요하다. 일반적으로 API 응답시간이 5초를 넘어간다면 잘못 개발되었을 확률이 높다.

#### ReadTimeout
- Timeout의 종류는 여러가지가 있다.
- 일반적으로 많이보이는 ConnectionTimeout, SocketTimeout 등등..
- 그런데 **ReadTimeout** 이란 무엇일까 ?

ReadTimeout 이란 그대로 직역하면 **무엇인가를 읽는데 시간을 초과**했다는 의미이다.

HTTP 환경에서의 ReadTimeout이란 바로 **서버로 요청을 보낸뒤 응답을 받는데까지 지정한 시간을 초과**했다는 것이다.

#### ReadTimeout을 지정하는 이유 ?
- ReadTimeout을 지정하는 이유를 알아보기에 앞서 익숙한 ConnectionTimeout을 지정하는 이유는 무엇일까 ?
- 데이터베이스의 커넥션, TCP 커넥션 등 커넥션을 맺는데 소요되는 시간의 임계치를 지정하는데, 만약 임계치가 지정되어있지 않은 상태일때
- 서버에서 맺을수 있는 커넥션의 수가 초과했다면, 커넥션을 맺기위해 **무한 대기** 상태에 빠지게 된다.

> 서버의 자원이 충분하던, 충분하지않던 서버와의 커넥션을 맺기위해 클라이언트는 무한 대기상태에 빠지게된다.

- 다시 돌아와서 ReadTimeout에 한번 대입해보게 되면 쉽게 답을 얻을 수 있다.
- ReadTimeout을 지정하지 않는다면, 서버로 요청을 보낸뒤 응답을 받을때 까지 **무한 대기 상태**에 빠지게 되기 때문에 이를 지정해주는것


#### ReadTimeout을 지정했을때에 문제점
- ReadTimeout을 지정하면, 지정한 시간 내에 응답을 받지 못할경우 연결을 끊어버린다.
- 이렇게 했을경우 발생하는 문제점은 과연 무엇일까 ?

주어진 상황은 다음과 같다.

1. 클라이언트가 OrderApi 를 통해 주문을 요청한다.
2. OrderApi는 Validation후 비즈니스로직을 수행하고, 해당 로직 내에는 결제와 관련된 로직은 PaymentApi 를 통해 처리를 해야한다.
3. OrderApi는 PaymentApi를 통해 카드사 결제 요청처리를 한다. (이때, ReadTimeout은 3초로 지정되어 있다고 가정)
4. OrderApi는 지정한 ReadTimeout인 3초가 될때까지 응답을 받지못해 결제가 되지않았다고 가정하고 연결을 끊어버린뒤 주문 실퍠를 클라이언트에게 알린다.
5. PaymentApi는 카드요청 처리를 10초를 소모하여 처리를 하였다. 하지만 OrderApi와의 연결이 끊어져 응답은 보내지 못한다.

> 사용자 입장에서는 카드사에서 결제는 되었지만, 주문은 들어가지 않는 기이한 상태가 되어버린다. 이런 문제를 해결하기 위해
적절한 ReadTimeout, 그에 따른 예외처리에 대한 고민이 필요하다.

#### 적절한 ReadTimeout은 ?
- HTTP 환경에서 API 통신을 한다고 가정했을때 일반적으로 3초 정도로 ReadTimeout을 지정한다. (절대적인 수치는 아님)
> API 응답까지 5초이상 걸리게 된다면 잘못 개발돤 API일 확률이 높다.
서버구성 환경, API가 처리할 리소스에 따라 이는 달라진다.

#### 정리
- ReadTimeout은 간단하 정리하면 클라이언트가 서버로 요청을 했을때, 서버로부터 응답을 받을때까지 기다릴 제한시간이다.
- ReadTimeout을 지정하지 않았을때, 지정하였을때 모두 문제점이 존재한다.
- 적절한 ReadTimeout 지정과, Timeout이 발생했을때 어떤식으로 처리해야하는지에 대한 고민이 필요하다.


  





# PSA 

PSA란 ? Portable Service Abstraction, 일관성 있는 서비스 추상화이다.
서비스 추상화의 가장 좋은 예는 JDBC이다.

JDBC라고하는 표준 스펙이 있기에 데이터베이스의 벤더에 종속되지않고 , 어떠한 데이터베이스를 사용하던
Connection, Statement, ResultSet을 이용하여 공통된 방식으로 코드를 작성할 수 있다.

데이터베이스 종류에 관계없이 같은 방식으로 제어가능한 이유는 어댑터패턴을 활용했기 때문이다.
이처럼 어댑터패턴을 활용해 같은 일을하는 다수의 기술을 공통 인터페이스로 제어 할 수 있게 한것을 서비스 추상화라고한다.



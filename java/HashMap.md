# HashMap

성능 = 	저장속도 가장느림
	검색 속도 가장빠름
멀티스레드 환경에서는 HashTable 사용

key , value 로 한쌍

value null 값 허용




# 해시충돌


해시맵에서 키로 사용되는 각종 자료형들에 대해 완벽한 해시 함수를 제공할 수는 없다.

서로가 구별되거나 Number객체는 객체가 나타내려는 값 자체를 해시 대상 값으로 사용할 수 있기 때문에 완전한 해시 함수 대상으로 삼을 수 있지만, String이나 POJO(plain old java object)에 대하여 완전한 해시 함수를 제작하는 것은 사실상 불가능 하다.

자바에서 해시값을 생성하는 메소드인 hashCode()의 결과 자료형은 int이다. 32비트 정수 자료형으로는 완전한 자료 해시 함수를 만들 수 없다.

객체의 수가 2의 32승보다 많을 수 있고, 모든 hashMap이 2의 32승만큼의 배열을 가지고 있을 수는 없기 때문


HashMap을 비롯한 많은 해시 함수를 이용하는 associative array(Dictionay, Map, Symbol Table 등) 구현체에서는 메모리 절약을 위해 실제 해시 함수의 표현 정수 범위 N보다 작은 M개의 원소가 있는 배열만을 사용한다. 

=======================
int index = X.hashCode() % M;  
======================

다음과 같이 객체에 대한 해시 코드의 나머지 값을 해시 버킷 인덱스 값으로 사용한다.

이런 방식을 사용하면, 서로 다른 해시 코드를 가지는 서로 다른 객체가 1/M의 확률로 같은 해시 버킷을 사용하게 된다. 이것이 자바의 해시 충돌 문제이다. 해시 함수 구현상의 문제가 아닌 또 다른 종류의 해시 충돌인 셈이다.


3) 해시 충돌 회피 방법



이런 충돌이 일어나도 키-값 쌍데이터를 안정적으로 저장하고 조회할 수 있도록 하는 대표적인 방법으로 두가지가 있다.

대표적으로 Open Addressing과 Separate Chaining이 있다.


첫 번째로 Open Addressing은 해시 충돌이 발생하면 다른 해시버킷에 해당 자료를 삽입하는 방식이다. 

두 번째인 Separate Chaining은 충돌 시 해당 버킷값을 첫 부분으로 하는 링크드 리스트로 해결한다.


첫 번째인 Open Addressing은 데이터 개수가 적다면 Separate chaining보다 더 성능이 좋다. 하지만 배열의 크기가 커질수록(M값) 연속된 공간에 데이터를 저장하여 캐시효율이 높다는 장점이 사라지게 되어 Separate chaining을 사용하는 것이 더 현명 해 보인다.

또한 remove()호출 빈도에 따라 효율이 달라진다. 삭제 처리 시 효율이 높은 linked list방식인 Separate chaining이 open addressing보다 remove() 메소드 호출이 잦은 HashMap에서 더 좋은 효율을 보인다.

자바는 HashMap에서 Separete Chaning방식을 채용하고 있다.

위에서 설명한 바와 같은 이유들로 왜 이방식을 채용하는 지는 충분한 이해가 될 것 같다.

4) 향상된 충돌 회피 (Java8)



최신 버전인 Java8에서는 더 향상된 방법을 사용하여 충돌을 회피한다.

이는 HashMap에 대한 지속적인 개발이 이뤄지고 있다는 것을 반증한다.

탐색에 있어 더 높은 효율을 보이는 트리를 접목시켰다

하나의 버킷에 충돌이 집중되는 현상을 해결하기 위한 방법으로 충돌된 키-값 쌍의 데이터가 8개가 모이면 링크드 리스트를 트리로 변경한다. 해당 값이 6개에 이르면 다시 링크드 리스트로 변경시킨다. 차이값이 8-7이 아니라 8-6인 이유는 잦은 링크드 리스트와 트리로의 변경으로 인한 성능저하를 막기 위함이라 한다.

하지만 트리의 특성 상 트리 순회 시 사용하는 판단 기준이 대소에 대한 구분이 있어야 하는데 이를 자바8에서는 레드 블랙 트리라는 것을 적용시켰다.

판단 기준으로 해시 함수 값을 사용하고 Total Ordering?을 해결하기 위해 tieBreakOrder()메소드로 해결한다.



[ 정리 ]

자바에서 말하는 해시충돌은 실제 해시 범위보다 적은 M만큼의 배열을 선언하여 메모리의 효율을 높였고 해시 값의 % M 값을 버킷값으로 삼아 이것이 충돌하는 것을 뜻한다.

해결 방법으로 Separate Chaining과 보조 해시 함수를 사용하고 자바8에서는 링크드 리스트 대신 트리(Red-black Tree)를 사용한다.


출처: http://odol87.tistory.com/4?category=586230 [IT 인생]

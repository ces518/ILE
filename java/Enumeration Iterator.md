# Enumeration


컬렉션 순차접근 객체. 자바 초기버젼부터 지원되며, HashTable or Vector에서취득 가능.
Enumeration은 해당 컬렉션의 값을 복사해서 활용하므로 활용 중에
해당 컬렉션의 값이 변경되어도 에러(ConcurrentModificationException) 발생(fail-fast)되지 않음.



# Iterator


컬렉션 순차접근 객체. 모든 컬렉션으로부터 취득 가능.
Iterator는 활용 중 해당 컬렉션의 추가, 삭제 작업으로인해
컬렉션 값이 변경되면 에러(ConcurrentModificationException)발생(fail-fast)되며,
모든 컬렉션이 이 경우에 해당되며, Enumeration만 제외됨. 

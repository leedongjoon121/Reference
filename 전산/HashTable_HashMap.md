### HashMap 과 HashTable
- 키에 대한 해시 값을 사용하여 값을 저장하고 조회하며, 키-값 쌍의 개수에 따라 동적으로 크기가 증가하는 associate array
- associate array를 지칭하기 위해서 HashTable에서는 Dictionary라는 이름을 사용, HashMap 에서는 Map 이라는 용어 사용
- Map 인터페이스를 상속받아 구현되어 데이터를 키와 값으로 관리

### Java HashMap
- HashMap은 Java Collections Framework에 속한 구현체 클래스


### HashMap 과 HashTable 차이점
```
둘의 가장 큰 차이점은 동기화 보장 유뮤, 키와 값에 null 가능 여부
동기화가 필요 없다면 HashMap, 동기화 보장이 필요하면 HashTable
동기화 보장 유무 차이 외에는 차이가 거의 없으며 자바 기준 사용법도 동일
```

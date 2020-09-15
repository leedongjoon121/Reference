### HashMap 과 HashTable
- 키에 대한 해시 값을 사용하여 값을 저장하고 조회하며, 키-값 쌍의 개수에 따라 동적으로 크기가 증가하는 associate array
- associate array를 지칭하기 위해서 HashTable에서는 Dictionary라는 이름을 사용, HashMap 에서는 Map 이라는 용어 사용

### Java HashMap
- HashMap은 Java Collections Framework에 속한 구현체 클래스

```
HashMap은 보조 해시 함수(Additional Hash Function)를 사용하기 때문에, 보조 해시 함수를 사용하지 않는 HashTable에 비해 해시 충돌(hash collision)이
덜 발생할 수 있어서 상대적으로 성능상 이점이 있음
```

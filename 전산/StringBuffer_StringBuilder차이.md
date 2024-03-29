# String, StringBuffer, StringBuilder 차이점 

String, StringBuffer, StringBuilder 이세개의 공통점은 String(문자열)을 저장하고 관리하는 클래스들이다.

### 불변 / 가변
#### 1. String : immutable(불변)  => new 연산을 통해 생성되면 그 인스턴스의 메모리 공간은 절대 변하지 않는다.

 - String은 new 연산을 통해 생성되면 그 인스턴스의 메모리 공간은 절대 변하지 않는다.
 
 - + 연산이나 concat을 이용해서 문자열에 변화를 줘도, 메모리 공간이 변하는 것이 아니라 새로운 String 객체를 new로 만들어서 새로운 메모리 공간 생성
 
 - 이렇게 새로운 문자열이 만들어지면 기존의 문자열은 가비지 콜렉터에 의해 제거되야 하는 단점(언제 제거될지 모름)이 있다.
 
 - => 또한 이러한 문자열 연산이 많아질 때 계속해서 객체를 만드는 오버헤드가 발생하므로 성능이 떨어질 수 밖에 없다는 단점 
 
 - => 대신 String 클래스의 객체는 불변하기 때문에 단순히 읽어가는 조회연산에서는 타 클래스보다 빠르게 읽을 수 있는 장점이 있다.
    (불변하기 때문에 멀티쓰레드환경에서 동기화를 신경쓸 필요가 없음)

- 결론 : String 클래스는 문자열 연산이 적고 조회가 많을 때 멀티쓰레드 환경에서 사용하면 좋다.


#### 2. StringBuffer, StringBuilder : mutable(가변) 
 
 - StringBuffer와 StringBuilder 클래스는 String과 다르게 mutable(변경가능)
 
 - 즉 문자열 연산에 있어서 클래스를 한번 만들고(new), 연산이 필요할 때 크기를 변경시켜서 문자열을 변경한다.
 
 - 그러므로 문자열 연산이 자주 있을 때 사용하면 성능이 좋다.
 
 - StringBuffer는 멀티쓰레드환경에서 synchronized키워드가 가능하므로 동기화가 가능하다, 
 
 - StringBuilder는 동기화를 지원하지 않기 때문에 멀티쓰레드환경에서는 적합하지 않다.
 
 - 대신 StringBuilder가 동기화를 고려하지 않기 때문에 싱글쓰레드 환경에서 StringBuffer에 비해 연산처리가 빠르다.
 
 - 결론 : 문자열 연산이 많을 때 멀티쓰레드 환경에서는 StringBuffer, 싱글 쓰레드 또는 쓰레드를 신경쓰지 않아도 되는 환경에서는 StringBuilder를 사용
 
### 결론
- String 클래스는 불변 객체이기 때문에, 문자열 연산이 많은 프로그래밍이 필요할 때 계속해서 인스턴스를 생성하므로 성능이 떨어지지만, 조회가 많은 환경, 멀티쓰레드 환경에서는 성능적으로 유리함.

- StringBuffer 클래스와 StringBuilder 클래스는 문자열 연산이 자주 발생할 때 문자열 변경이 가능한 객체이기 때문에 성능적으로 유리

- StringBuffer와 StringBuilder의 차이점은 동기화지원의 유무이고, 동기화를 고려하지 않는 환경에서 StringBuilder가 성능이 더 좋고, 동기화가 필요한 멀티 쓰레드 환경에서는 StringBuffer를 사용하는 것이 유리함





### 해시 테이블

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/hashTable.png?raw=true)

해시테이블은 해시함수를 사용하여 키를 해시값으로 매핑하고, 이 해시값을 색인 또는 주소삼아 데이터(value)를 key와 함께 저장하는 자료구조

### 해시테이블 구성

#### key
- 고유한 값, hash function의 input이 된다.
- 키값 그대로 저장소에 저장할 경우 다양한 키의 길이 만큼의 크기를 구성해두어야 하기 때문에 일정한 길이의 해시로 변경한다.

#### hash function
- key를 고정된 길이의 hash로 변경해주는 역할을 한다. 이 과정을 hashing이라고 한다.
- 서로 다른 key가 같은 hash값을 갖게 되는 경우 이를 해시 충돌 이라고 한다. 해시 충돌 발생 확률이 적을 수록 좋다.

```
해시충돌이 해시값 전체에 걸쳐 균등하게 발생하도록 하는 것도 중요하다. 모든 키가 02라는 동일한 해시값으로 매핑이 될 경우
데이터를 액세스할 때 비효율성이 커지고, 보안이 취약(서로 다른 키인데도 동일한 해시값)해져 
굳이 해시를 도입해 데이터를 관리할 이유가 없어진다.
```
#### value
- 저장소(bucket, slot)에 최종적으로 저장되는 값으로, hash와 매칭되어 저장.

#### hash table
- 해시함수를 사용하여 키를 해시값으로 매핑하고, 이 해시값을 색인 또는 주소 삼아 데이터(value)를 key와 함께 저장하는 자료구조
- 데이터가 저장되는 곳을 버킷 또는 슬롯이라고 한다.
- 해시 테이블의 기본 연산은 삽입, 삭제, 탐색이다.

key는 hash function을 통해 hash로 변경이 되며 hash는 value와 매칭되어 저장소에 저장이 된다.

### 장점
- 해시테이블은 key-value가 1:1로 매핑되어 있기 때문에 삽입, 삭제, 검색의 과정에서 모두 평균적으로 O(1)의 시간복잡도를 가지고 있다.

### 단점
- 해시 충돌이 발생
- 순서/관계가 있는 배열에는 어울리지 않는다 => 순서에 상관없이 key만을 가지고 삽입, 검색, 삭제하기 때문
- 공간 효율성이 떨어짐 => 데이터가 저장되기 전에 미리 저장공간을 확보해야하기 때문. 공간이 부족하거나 아예 채워지지 않은 경우가 발생
- hash function의 의존도가 높다 => 평균 시간복잡도가 O(1)이지만 해시함수가 매우 복잡하다면 해시테이블의 연산 속도는 증가


### HashTable 크기에 대한 고찰

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/hashTableSize.png?raw=true)

```
키의 전체 개수와 동일한 크기의 버킷을 가진 해시테이블을 Direct-address table라고한다.
Direct-address table의 장점은 키의 개수와 테이블의 크기가 같기 때문에 해시 충돌 문제가 발생하지 않는다는 것이다.
하지만 실제 사용하는 키는 몇개 되지 않을 경우에는? 전체키 100개중에 실제로는 10개의 키만 사용하는데 100개 크기의 
테이블을 유지하고 있는 것은 메모리 낭비이다.

따라서 보통의 경우 실제 사용하는 키 개수보다 적은 해시테이블을 운용한다고 한다. 그렇기에 해시 충돌이 발생할 수 밖에 없고, 
해시 충돌을 해결하기 위한 다양한 방법들이 고안되었다.
```

<hr/>
<hr/>

## 해시충돌

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/hashCollision.png?raw=true)

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/hashCollision2.png?raw=true)

```
John과 Sandra의 hash가 2로 같다. 이런 현상을 hash collision이라고 한다.

해시 함수로 해시를 만드는 과정에서 서로 다른 key가 같은 해시로 변경되면 같은 공간에 2개의 value가 저장되므로
key-value가 1:1로 매핑되어야 하는 해시 테이블의 특성에 위배된다.
해시 충돌은 필연적으로 나타날 수 밖에 없다.

```

## 해시충돌 해결방법

### 1. Chaining

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/hashCollisionResolve1.png?raw=true)


체이닝은 저장소(bucket)에서 충돌이 일어나면 기존 값과 새로운 값을 연결리스트를 이용해 연결시키는 방법이다.

### 장점

- 한정된 저장소를 효율적으로 사용할 수 있다 => 미리 충돌을 대비해 많은 공간을 잡아놓을 필요가 없다
- 해시 함수를 선택하는 중요성이 상대적으로 적다 => 충돌이 나도 그냥 연결해주면 되니까

### 단점

-한 hash에 자료들이 많이 연결되면 검색 효율이 낮아진다(쏠림 현상)
- 외부 저장 공간을 사용한다 => 왜?


### 2. Open Addressing(개방주소법)

개방주소법은 비어있는 hash를 찾아 데이터를 저장하는 기법이다. 따라서 개방주소법의 해시 테이블은 hash와 value가 1:1관계를 유지한다.

## ![사진](https://github.com/leedongjoon121/Reference/blob/img/img/hashCollisionResolve2.png?raw=true)

```
위의 그림에서 John과 Sandra의 hash가 동일해 충돌이 일어난다. 이때 Sandra는 바로 그 다음 비어있던 153 hash에 값을 저장한다. 그 다음 Ted가 테이블에 저장을 하려 했으나 본인의 hash에 이미 Sandra로 채워져 있어 Ted도 Sandra처럼 바로 다음 비어있던 154 hash에 값을 저장한다.

이런 식으로 충돌이 발생할 경우 비어있는 hash를 찾아 저장하는 방법이 개방주소법이다. 이때, 비어있는 hash를 찾아가는 방법은 여러가지가 있다.
```


<hr/>

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

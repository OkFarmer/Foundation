# vector와 Stack을 사용하지 못하는 이유를 설명해주세요.

C++ STL중 Vector는 Stack과 다르게 random access가 가능하고, iterator 등 구성 원소에 접근이 용이한 여러 기능을 가지고 있어 널리 쓰인다.

Vector로 Stack형 자료구조를 구현하게 된다면 스택의 꼭대기가 아닌 맨 아래에 있는 원소를 참조할 수도 있고, 중간 부분에 원소를 추가하는 것 또한 가능하다.

C++에서 Vector와 Stack은 사용자의 요구에 맞게 상황에 맞게 서로 혼용될 수 있는 편리한 STL인 것이다.

Java에서도 Vector 와 Stack 컬렉션 프레임 워크를 가지고 있지만 아직 사용하는 사람들이 있어 Deprecated 되지만 않았을 뿐, 사실 둘 다 가급적 쓰여서는 안되는 컬렉션이다.

---

### Vector

Vector는 get()과 set()역할을 하는 모든 메서드에 synchronized 키워드가 붙어 있다. Vector의 모든 get() set() 등의 메서드에 synchronized가 붙어있는건 특정 상황에서 성능을 꽤 저하시킬 수 있다.

<img width="675" alt="image" src="https://user-images.githubusercontent.com/76817418/160975378-3899f2b6-56ed-49cb-a373-1ecd465d485a.png">

<img width="680" alt="image" src="https://user-images.githubusercontent.com/76817418/160975346-3423baf3-daa6-4b88-a07e-ef0a80228419.png">

단순히 Vector에 Iterator를 붙여 순차적으로 item들을 탐색하기만 해도 원소탐색 시마다 get() 메서드의 실행을 위해 계속 lock을 걸고 닫으므로 Iterator연산과정 전체에 1번만 걸어주면 될 locking에 쓸데없는 오버헤드가 엄청나게 발생한다.

Vector는 특정 상황에서만 최적으로 동작하게 되고, 어떤 상황에서는 그렇지 않게 되므로 효율적인 Thread-safe 컬렉션이라고 할 수 없는 것이다.

따라서 멀티스레드 프로그래밍을 하는게 아니라면 비슷한 역할을 하는 ArrayList를 사용하는 것이 좋다. 

멀티스레드 환경일 때도 Vector 보다는 ArrayList를 사용하는게 좋은데 

```java
ArrayList<T> al = new ArrayList<>(Collections.synchronizedList());
```

이와 같이 ArrayList의 생성자에 매개변수로 Collections.synchronizedList()를 넘겨주게되면 thread-safe한 ArrayList를 사용할 수 있다.

---

### Stack

Stack 또한 Vector를 상속받기 때문에 Vector의 기능을 전부 사용할 수 있게된다.

<img width="240" alt="image" src="https://user-images.githubusercontent.com/76817418/160975309-937d4b9f-489d-43e9-939c-f62ac69eee41.png">

이는 Stack STL이 완벽한 LIFO 구조를 가질 수도 없게되고, 앞서 말한 Vector의 모든 단점을 그대로 물려받게 되는 것이다.

Stack을 대체할 컬렉션 프레임워크로는 Deque가 있다. 

<img width="680" alt="image" src="https://user-images.githubusercontent.com/76817418/160975288-5bc529e9-4eb0-4963-aae2-368cd33d247c.png">

자바에서 Deque를 구현하는 방법은 크게 LinkedList와 ArrayDeque가 있는데, 스택의 size가 엄청 커질 가능성이 있고 size의 변동성이 매우 큰 경우 즉각적인 메모리 공간 확보를 위해선 LinkedList방식이 적절하고, 그렇지 않은 경우는 자체 메모리 소모량이 적고 iterate의 효율이 좋은 ArrayDeque를 사용하면 된다.

그 외 특수한 상황을 더 고려해보자면, 멀티스레드 환경에서는 ConcurrentLinkedDeque를 사용하는게 좋고, 스택의 size가 제한되어있는 경우에 LinkedBlockingDeque를 사용하는 것을 고려해볼만 하다.

> Java의 Vector와 Stack은 멀티스레드 환경의 여부와 상관없이 대부분의 조건에서 성능 저하를 일으킨다.
> 
> 
> Vector가 필요한 상황이라면 대신 ArrayList를 사용하는 것이 바람직하다.
> 
> 마찬가지로 Stack 대신 Deque의 하위컬렉션을 상황에 맞게, 혹은 그냥 ArrayList를 사용하는 것이 적절하다.
> 

[참고][https://aahc.tistory.com/8](https://aahc.tistory.com/8)
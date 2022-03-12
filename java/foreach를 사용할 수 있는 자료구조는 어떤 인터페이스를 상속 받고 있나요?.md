# foreach를 사용할 수 있는 자료구조는 어떤 인터페이스를 상속 받고 있나요?

- foreach 문은 Iterator 인터페이스를 상속받기 때문에 컬렉션과 배열은 물론 `Iterable`
 인터페이스를 구현한 객체라면 무엇이든 순회할 수 있습니다.

- for-each 문은 for 문(enhanced for statement)이라는 정식 명칭을 가지고 있으며 반복자와 인덱스 변수를 사용하지 않아 코드가 깔끔하고 잘못된 변수 사용으로 오류가 발생할 일도 없습니다.

## 반복문의 사용

기존의 컬렉션 자료형에서 자료를 추출해낼 때는 크게 다음과 같은 방법을 써왔습니다. 

- for문 사용 : index 있는 경우 가능
- Enhanced-for 사용 : index 없는 경우도 사용 가능
- Iterator 객체 사용

그런데 JAVA8부터 forEach()라는 메서드를 통해 더욱 간단하게 추출이 가능해졌습니다.

```java
public class MyClass {
    private int id;
    private String name;
    
    public MyClass() {}
    public MyClass(int id, String name) {
        this.id = id;
        this.name = name;
    }
    
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    
    public void displayInfo() {
        System.out.println("학번: " + id);
        System.out.println("이름: " + name);
    }
    
    public static void display(MyClass c){
        c.displayInfo();
    }
    
    @Override
    public String toString() {
        return "학번: " + id + "\n" + "이름: " + name;
    }
} // end class MyClass
```

먼저 학번(id)와 이름(name)으로 구성된 MyClass를 정의하고

Hash Set을 사용하여 MyClass의 add된 인스턴스를

Iterator 를 사용해서 출력해보고

Enhanced-for 를 사용해서 출력해보고

그리고 forEach() 를 사용해서 출력해봅니다.

```java
public static void main(String[] args) {
        System.out.println("HashSet 연습");
        
        // MyClass 타입을 저장할 수 있는 HashSet 인스턴스 생성
        HashSet<MyClass> hset = new HashSet<MyClass>();
        
        // 데이터 3개 저장
        MyClass mc1 = new MyClass(1, "Abc");
        MyClass mc2 = new MyClass(2, "Def");
        MyClass mc3 = new MyClass(3, "Asdf");
        hset.add(mc1);
        hset.add(mc2);
        hset.add(mc3);
        
        //Iterator
        System.out.println();
        System.out.println("Iterator");
        Iterator<MyClass> itr = hset.iterator();
        while (itr.hasNext()) {
            //System.out.println(itr.next());
            MyClass mc = itr.next();
            System.out.println("id: " + mc.getId());
            System.out.println("name: " + mc.getName());
        } // end while
        
				//enhanced for
        System.out.println();
        System.out.println("enhanced for");
        // for (자료타입 변수명 : 배열/리스트/셋) {}
        for (MyClass m : hset) {
            m.displayInfo();
        }
        
        // forEach() 메소드 사용
        System.out.println();
        System.out.println("forEach() 사용");
        hset.forEach(System.out::println);  // toString 을 오버라이드 하여 println 으로도 출력 가능
        hset.forEach(MyClass::display);        // static 메소드인 display 
    }
```

hset.forEach(System.out::println)  는  다음과 같이 작동하고  

    for( Myclass c : hset ){      
        System.out.printnl(c);          
    }

hset.forEach(MyClass::display) 는 다음과 같이 작동합니다

    for( Myclass c : hset) {
        MyClass.displayl(c);
    }

forEach() 는 Iterable<E> 인터페이스를 구현한 모든 클래스에서 사용 가능하고 상당한 코딩량 감소 효과를 가져올수 있습니다. 

여기서 콜론(:)은 “안의(in)” 라고 읽습니다. 위 코드는 “arr 배열 안의 각 원소 element” 라고 읽으면 되겠네요. 한편 컬렉션을 중첩하여 2중으로 순회해야 한다면 `for-each` 문의 장점은 더 커집니다.

```java
// 2중 for each
for (Suit suit : suits) {
    for (Rank rank : ranks) {
        deck.add(new Card(suit, rank));
    }
}
```

### **for-each를 사용할 수 없는 상황**

아쉽게도 `for-each` 문장을 사용할 수 없는 상황이 있습니다.

**필터링: Filtering,** 컬렉션을 순회하면서 선택된 엘리먼트를 제거해야 한다면 아래와 같이 반복자(iterator)를 명시적으로 사용해야만 합니다. remove 메서드를 호출해야 하기 때문인데요.

**foreach** 문장을 사용하여 리스트 자체를 수정하게 되는 경우에는 `ConcurrentModificationException`이 발생할 겁니다. 기본적으로 리스트는 순회중인 상태에서 자기 자신에 대한 삭제와 같은 변경을 할 수 없게 되어 있습니다. 따라서 `Iterator`를 사용해야 합니다.

```java
// some list
List<String> list = new ArrayList<>();
list.add("a"); list.add("b"); list.add("c");

for (Iterator<String> iterator = list.iterator(); iterator.hasNext(); ) {
    String element = iterator.next();
    if(element.equals("a")) {
        iterator.remove();
    }
    // do something
}
```

하지만 `Java 8` 부터는 Collection의 `removeIf` 메서드를 이용하여 컬렉션을 명시적으로 순회하지 않아도 됩니다.

```java
// Lambda
list.removeIf(s -> s.equals("a"));

// 위 코드를 풀어서 표현하면,
list.removeIf(new Predicate<String>() {
    @Override
    public boolean test(String s) {
        return s.equals("a");
    }
});
```

**변형: Transforming,** 그리고 순회하면서 그 원소의 값 일부나 전체를 변경해야 한다면 반복자 혹은 배열의 인덱스를 사용해야 합니다.

```java
// some array
String[] arr = new String[]{"a", "b", "c"};

// index를 사용할 수 밖에 없다.
for (int index = 0; index < arr.length; index++) {
    String s = arr[index];
    if(s.equals("a")) {
        arr[index] = "d";
    }
}
```

**병렬 순회: Parallel iteration,** 마지막으로 여러 개의 컬렉션을 병렬적으로 순회해야 한다면 각각의 반복자와 인덱스 변수를 사용하여 엄격하고 명시적으로 제어해야 합니다. 그렇지 않으면 아래와 같은 문제가 발생할 수 있습니다.

```java
enum Suit {
    CLUB, DIAMOND, HEART, SPADE
}

enum Rank {
    ACE, DEUCE, THREE, FOUR,
    // ... 생략
    QUEEN, KING
}

List<Card> deck = new ArrayList<>();
List<Suit> suits = Arrays.asList(Suit.values());
List<Rank> ranks = Arrays.asList(Rank.values());
for (Iterator<Suit> i = suits.iterator(); i.hasNext(); ) {
    for (Iterator<Rank> j = ranks.iterator(); j.hasNext(); ) {
        // next 메서드가 숫자(suit) 하나당 불려야 하는데
        // 카드(Rank) 하나당 불리고 있다.
        deck.add(new Card(i.next(), j.next()));
    }
}
```

반복자의 `next` 메서드가 Suit를 탐색하는 루프 1회마다 불려야 하는데, Rank를 탐색하는 루프가 수행될 때마다 불리고 있어서 결국 모든 숫자(Suit)를 탐색하게 되어 `NoSuchElementException`이 발생하게 됩니다.

위에서 살펴본 상황에 속하게 될 경우 일반적인 for 문을 사용해야 합니다.

출처: https://bitsoul.tistory.com/57 [Happy Programmer~]

출처: [https://madplay.github.io/post/prefer-foreach-loops-to-traditional-for-loops](https://madplay.github.io/post/prefer-foreach-loops-to-traditional-for-loops)
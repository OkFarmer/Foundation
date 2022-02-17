
# iterable이란

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbE4TfJ%2FbtqBh1w4sLx%2FicJkqcLkLArocYCR4rHUFK%2Fimg.png)
- collection 인터페이스의 상위 인터페이스
- iterator() 메소드가 추상메소드로 선언되어있다
- iterable의 역할은 하위클래스에서 iterator()을 구현하게 만드는 것이다

- Iterator 인터페이스
    public interface Iterable<T>
    {
        Iterator<T> iterator();
    }


---
# iterator 인터페이스

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FAxXDw%2FbtqCLMqdXdQ%2FMI3Mgh8EddfpzJ7l3TKPL0%2Fimg.png)
- *Java 컬렉션 클래스의 데이터를 하나씩 읽어올 때 사용
- 표준화되어있지 않은 클래스의 데이터들을 공통 인터페이스를 정의해서 표준화하는것
- 인터페이스를 상속받은 List, Set은 hasNext(), next(), removed() 등의 메소드를 사용할 수 있다
- 인터페이스를 상속받지 않은 Map은 entrySet()을 통해 사용한다 
- iterator()를 호출하면 iterator 객체 반환
- 리스트 구조의 컬렉션에서 요소의 순차검색을 위한 메소드 포함

- 어떤 컬렉션이라도 동일한 방식으로 접근이 가능하여 그 안의 항목에 접근할 수 있는 방법 제공(다형성) =>  코드의 일관성을 유지하여 재사용성을 극대화할 수 있다.

- Iterator의 메소드 
    public interface Iterator<E>
{
    * 메소드 호출 순서대로
    1. boolean hasNext() : 다음 요소에 읽어 올 요소가 있는지 확인 하는 메소드 있으면 true, 없으면 false 를 반환한다
    2. E next();  : 다음 요소를 가져온다
    3. void remove(); : next()로 가져온 element를 삭제할 수 있다
}


* Java Collection Framework?
    데이터를 저장하는 클래스들을 표준화한 설계
    Set, List, Map 등을 포함
    Collection Interface : Set, List 등

## iterator 사용 예시
- List<String> list = new ArrayList<>(Arrays.asList("1", "2", "3"));

    Iterator<String> itrt = list.iterator();
    while (itrt.hasNext()) {
        System.out.print(itrt.next());
    }
    // 출력
    123

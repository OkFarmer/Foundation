# Interface와 Abstract Class
- 공통점 ! 둘다 상속받는 클래스에서 추상 메소드를 반드시 구현한다
- 차이점 ! 목적이 다르다. Abstract Class는 기존 클래스의 공통부분을 추상화하여 자식클래스에게 구현을 강제화하고 기능의 이용과 확장에 목적이 있고 Interface는 구현내용이 없는 뼈대 메소드를 통해 상속받는 클래스에서 구현을 강제한다. 즉 Abstract Class는 상속, Interface는 다형성의 개념이다
- 구분하는 이유 !  자바가 다중 상속을 지원하지 않는다. 다중상속의 모호성때문에 아예 막아놓았고 Interface를 사용해서 다중 구현을 보완할 수 있다.



## Interface

- 인터페이스는 클래스가 아니고 상속받는 클래스에서 구현한다
- 상속받는 클래스들 사이 관련이 없을 수 있다
- 구현을 강제시켜 인터페이스를 구현한 객체의 동일한 동작을 보장

- 인터페이스의 제약사항
    - 모든 멤버변수는 public static final (생략가능)
    - 모든 메서드는 public abstract 추상메소드 (생략가능)

- 다중상속이 가능하다</br>
    ```java
    class car implements vehicle,engine
        @Override
        public void drive(){
            @doSomething
        } 
    }
    ```


## Abstract Class

- 추상메소드란 선언부는 있는데 구현부가 없는 메소드를 의미하고 추상메소드를 포함한 클래스가 추상클래스
- 인스턴스,객체를 만들 수 없는 클래스

- 부모 클래스의 역할을 하기 때문에 공통점이 있는 다른 클래스들이 상속받아 구현할 수 있다
- is kind of 관계
    
- 다중상속이 불가능하다.</br>
    ```java
    class MyVehicle extends car,plane{
        @Override
        public void go(){
            super.driver();
        } 
    }
    ```

참고
https://loustler.io/languages/oop_interface_and_abstract_class/
https://devlog-wjdrbs96.tistory.com/370
https://brunch.co.kr/@kd4/6

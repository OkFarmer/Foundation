# Wrapper Class란 무엇이고 Primitive Type과의 차이는 무엇인가요?

Primitive Type : int, long

wrapper Class : Integer, Long, String

<img width="600" alt="image" src="https://user-images.githubusercontent.com/76817418/154613108-1bb796f3-9374-4842-ab39-4a9679f87685.png">

### Primitive type?

- 특정값을 보유할 수 있는 기본형타입이다.
- 기본값이 있기 때문에 NULL이 존재하지 않는다.
- 실제 값을 저장하는 공간으로 스택(Stack) 메모리에 저장된다.
- 만약 컴파일 시점에 담을 수 있는 크기를 벗어나면 에러를 발생시키는 컴파일 에러가 발생한다.

### Wrapper Class 란 ?

- 참조 유형으로 객체가 저장된 데이터 위치에 대한 포인터 이므로 null 객체도 참조 가능하다.
- 객체가 기본 데이터 유형을 저장할 수 있는 특정 유형의 클래스
- 원시 데이터 자료형과는 다르기 때문에 메소드에 접근이 불가능하다.
- 래퍼 클래스를 사용하면 다양한 작업에 메서드를 사용하는 래퍼 객체를 만들 수 있다.

래퍼 클래스(Wrapper class)는 산술 연산을 위해 정의된 클래스가 아니므로, 인스턴스에 저장된 값을 변경할 수 없다.

단지 값을 참조하기 위해 새로운 인스턴스를 생성하고, 생성된 인스턴스의 값만을 참조할 수 있다. 
<p align=center><img width="300" alt="image" src="https://user-images.githubusercontent.com/76817418/154613230-78a17b69-921a-4077-a93b-960985c43cb1.png"></p>

위의 그림과 같이 기본 타입의 데이터를 래퍼 클래스의 인스턴스로 변환하고,반대로 꺼내는 과정을 박싱(Boxing), 언박싱(UnBoxing)이라고 한다.

```java
Integer num = new Integer(17);  //박싱
int n = num.intValue(); //언박싱

Character ch = 'X'; //Character ch = new Character('X'); : 오토박싱
char c = ch;    //char c = ch.charValue();  : 오토 언박싱
```

### 참조형 타입(Reference type) ⇒ Wrapper Class

- 기본형 타입을 제외한 타입들이 모두 참조형 타입(Reference type)이다.
- 빈 객체를 의미하는 Null이 존재한다.
- 값이 저장되어 있는 곳의 **주소값**을 저장하는 공간으로 **[힙(Heap)](http://gbsb.tistory.com/2?category=674290#java-memory)** 메모리에 저장된다.
- 문법상으로는 에러가 없지만 실행시켰을 때 에러가 나는 런타임 에러가 발생한다. 예를 들어 객체나 배열을 Null 값으로 받으면 NullPointException이 발생하므로 변수값을 넣어야 한다.


```java
public class test {
    public static void main(String args[]){
        //primitive type
        int a1=3;
        int b1=3;
        System.out.println(a1==b1); //true
        
        //Wrapper class
        Integer a2= new Integer(3); 
        Integer b2 = new Integer(3);
        System.out.println(a2==b2); //false => 객체를 가리키는 포인터의 주소가 다르다.
        System.out.println(a2.equals(b2));  //true => equal 메소드는 객체가 위치한 주소의 value를 비교한다.
        
        //Wrapper class unboxing
        Integer a3=3;   //컴파일러가 다음과 같이 변환합니다. : Integer a = Integer.valueOf(3); => auto unboxing    
        Integer b3=3;   //컴파일러가 다음과 같이 변환합니다. : Integer b = Integer.valueOf(3);
        System.out.println(a3==b3); //true  => a3과 b3이 동일한 Object를 가지고 있다. 
    
        
        System.out.println(a1==a2); //true
        System.out.println(a1==a3); //true
    }
}

```

위에서 볼 수 있듯이 Integer(int) Wrapper class는 java9 이상의 버전에서  권장하지 않는 방법이라고 뜬다. 

![image](https://user-images.githubusercontent.com/76817418/154614832-a80aa563-7ec7-4434-b779-a3cb0bd69f22.png)
[Integer API 문서](https://docs.oracle.com/javase/9/docs/api/java/lang/Integer.html)
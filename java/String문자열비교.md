
    String은 일반적인 타입이 아닌 클래스이기 때문에 call by Reference형태로 생성시 주소값이 부여된다. 

그렇기 때문에 String타입을 선언했을 때 같은 값을 부여하더라도 서로간의 주소값이 다를 수 있다. 

자바에서 문자열(String)을 선언하는 방법은 아래와 같다. 

```java
String str1 = "madplay";  //문자열 리터럴 생성방식
String str2 = "madplay";
String str3 = new String("madplay");  //생성자인 new 연산자를 이용한 문자열 방식
String str3 = new String("madplay");
```

- new연산자를 통해 문자열 객체를 생성하는경우
    
    메모리의 Heap영역에 할당
    
- 문자열 리터럴 생성하는 경우
    - String Constant Pool영역에 할당
        
        상수풀(String Constant Pool)의 위치는 java7부터 Perm영역에서 Heap 영역으로 옮겨졌다. Perm영역은 실행시간(Runtime)에 가변적으로 변경할 수 없는 고정된 사이즈이기 때문에 intern메서드의 호출은 저장할 공간이 부족하게 만들 수 있었다. 즉 OOM(Out Of Memory) 문제가 발생할 수 있는 위험이 있었던 것이다.
        
        Heap 영역으로 변경된 이후에는 상수풀에 들어간 문자열도 Garbage Collection 대상이 된다.
        
    

문자열을 리터럴과 new 연산자로 생성하는 경우 heap영역에 매핑된다. 

![](https://images.velog.io/images/hweyoung/post/73110d50-bab4-476f-a312-e81ce0a7c423/image.png)


문자열 리터럴의 경우 내부적으로 String의 intern메서드를 호출하게 된다. 

intern메서드는 해당 문자열이 String Constant Pool에 이미 있는 경우에는 그 문자열의 주소값을 반환하고 없다면 새로 집어넣고 그 주소값을 반환한다. 

### 문자열을 비교해보자 (.equals)vs(==)

```java
public class test {
    public static void main(String[] args){
        String s1 = "abcd";
        String s2 = "abcd";
        String s3 = new String("abcd");

        System.out.println(s1==s2);
        System.out.println(s1==s3);
        System.out.println(s1.equals(s2));
        System.out.println(s1.equals(s3));
    }
}
```

![](https://images.velog.io/images/hweyoung/post/491abe93-dcde-44af-abd5-59b4bc34fc70/image.png)

동일하게 "abcd"라는 문자열을 선언하였는데 String의 equals 메소드로 비교한 경우는 true, ==연산으로 비교한 경우는 false가 반환된다. 

equals 메소드는 String 클래스의 메소드이다. 매개변수로 객체의 참조변수를 비교하여 두 대상의 값 자체를 비교하고 boolean으로 반환한다. 
아래의 코드는 String 클래스의 equals메소드이다. 
![](https://images.velog.io/images/hweyoung/post/e82dcd02-043e-490c-9114-71d384141df3/image.png)


==연산은 객체의 주소값을 비교한다. 

⇒ new 연산자를 통해 heap영역에 생성된 String 과 리터럴을 이용해 String Constant Pool영역에 위치한 String의 주소값은 같을 수가 없다.
    
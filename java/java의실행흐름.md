
# JVM은 어떤 방식으로 코드를 해석하고 실행시키는지 흐름에 맞게 설명해 주세요. (Java 실행 흐름)

![](https://images.velog.io/images/hweyoung/post/0ab5b6ce-534d-4813-90a8-e5ec9f3ac245/image.png)
자바는 os에 독립적인 특징을 가지고 있다. 이게 가능한 이유는 JVM(java virtual machine)이 os와 프로그램의 사이에서 기계어로 해석해주는 역할을 하기 때문이다. 
자바 컴파일러에 의해 변환된 java 바이트 코드(.class)는 os에 의존하지 않고 JVM위에서 작동한다.
jvm은 운영체제에 종속적이기 때문에 해당하는 os에 맞는 jvm설정을 해줘야 한다. 

---
![](https://images.velog.io/images/hweyoung/post/7e167fe9-c34a-43ab-a842-e7633b2c0ae7/image.png)

#### 자바의 동작 방법
hello.java -> javac.exe(자바 컴파일러) -> hello.class생성 -> java.exe(자바 인터프리터) -> "hello world"출력
### 자바 컴파일 순서 
1. 개발자가 자바 소스코드(.java)를 작성한다.

2. 자바 컴파일러(Java Compiler)가 자바 소스파일을 컴파일한다.
이때 나오는 파일은 자바 바이트 코드(.class)파일로 아직 컴퓨터가 읽을 수 없는 자바 가상 머신이 이해할 수 있는 코드이다. 바이트 코드의 각 명령어는 1바이트 크기의 Opcode와 추가 피연산자로 이루어져 있다.

3. 컴파일된 바이트 코드를 JVM의 클래스로더(Class Loader)에게 전달.

4. 클래스 로더는 동적로딩(Dynamic Loading)을 통해 필요한 클래스들을 로딩 및 링크하여 런타임 데이터 영역(Runtime Data area), 즉 JVM의 메모리에 올린다.

#### 클래스 로더 세부 동작
-  로드 : 클래스 파일을 가져와서 JVM의 메모리에 로드한다.
- 검증 : 자바 언어 명세(Java Language Specification) 및 JVM 명세에 명시된 대로 구성되어 있는지 검사한다.
- 준비 : 클래스가 필요로 하는 메모리를 할당(필드, 메서드, 인터페이스 등등)
- 분석 : 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경한다.
- 초기화 : 클래스 변수들은 적절한 값으로 초기화한다.(static 필드)
![](https://images.velog.io/images/hweyoung/post/0c48104e-e8e7-46f9-a1bf-14b7211f5e7e/image.png)
5. 이렇게 생성된 자바 바이트 코드(.class)는 클래스 로더에 의해서 JVM내로 로드 되고, 실행엔진에 의해 기계어로 해석되어 메모리 상(Runtime Data Area)에 배치되게 됩니다.
실행엔진(Excutetion Engine)에는 Interpreter와 JIT(Just-In-Time) Compiler가 있습니다. 
- Interpreter : 바이트 코드를 한 줄씩 읽기 때문에 실행이 느리다.
- JIT : 인터프리터의 단점을 보완함, 전체 바이트 코드를 컴파일 하고 해당 코드를 직접 실행. 인터프리팅 방식보다 속도가 느림, 하지만 캐시 사용으로 한번 컴파일 한 후에는 빠르게 수행됨

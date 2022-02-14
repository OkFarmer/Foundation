# LinkedList와 ArrayList의 차이는 무엇일까?
Linkedlist와 Arraylist는 둘 다 List인터페이스를 상속받아서 구현한 클래스이다. 

---
## ArrayList
원소들을 인덱스로 접근하여 배열과 사용법이 매우 유사합니다.
![](https://images.velog.io/images/hweyoung/post/897e0d46-e72e-42f6-b719-c9d1133d6e9c/image.png)

배열은 초기에 생성할 때 크기를 정해줘야 하므로 유동적인 사이즈로 초기화할 수 없는 불편함이 있지만
대안으로 쓰이는 ArrayList는 저장되는 데이터의 갯수에 따라 자동적으로 크기가 변경되어 배열대신 자주 사용합니다.

배열은 크기를 변경할 수 없는 인스턴스이므로, 크기를 늘리기 위해서는 새로운 배열을 생성하고 기존의 요소들을 옮겨야 하는 복잡한 과정을 거쳐야 합니다.
![](https://images.velog.io/images/hweyoung/post/aed7b797-e224-41bb-9154-7807e9af98c8/image.png)

물론 이 과정은 자동으로 수행되지만, 요소의 추가 및 삭제 작업에 걸리는 시간이 매우 길어지는 단점을 가지게 됩니다.



---
## Linkedlist
ArrayList와 장단점이 비교되는 리스트입니다.

LinkedList는 각각의 데이터가 노드로 구성되어 연결이 되는 구조입니다.
![](https://images.velog.io/images/hweyoung/post/efb0dcdd-6210-40c8-a8cd-08f9e32ef6cc/image.png)
단일 연결 리스트는 요소의 저장과 삭제 작업이 다음 요소를 가리키는 참조만 변경하면 되므로, 아주 빠르게 처리될 수 있습니다.

하지만 단일 연결 리스트는 현재 요소에서 이전 요소로 접근하기가 매우 어렵습니다
일반적으로 LinkedList의 장점은 원소가 삽입되고 삭제될 때 바로 앞에 있는 원소의 링크값만을 변경하면 되기 때문에 데이터를 추가하거나 삭제하는 것이 원활하다는 점입니다.

LinkedList 클래스 역시 List 인터페이스를 구현하므로, ArrayList 클래스와 사용할 수 있는 메소드가 거의 같습니다

---
### ArrayList와 LinkedList의 장단점
- 순차적으로 추가/삭제하는 경우에는 ArrayList가 LinkedList보다 빠르다.
ArrayList의 경우 배열의 공간이 충분한 상황에서 값을 추가할 때는 비어있는 공간의 마지막 인덱스에 값을 넣어주면 되기 때문에 빠르고, 순차적으로 마지막 데이터부터 삭제할 경우 각 요소들의 재배치가 필요하지 않기 때문에 상당히 빠르다.
그렇지만 ArrayList의 크기가 충분하지 않으면 값을 추가할 때 새로운 크기의 ArrayList 배열을 생성하고 데이터를 복사하는 일이 발생하기 때문에 LinkedList가 더 빠를 수 있다. 

- 중간 데이터를 추가/삭제하는 경우에는 LinkedList가 ArrayList보다 빠르다. 
LinkedList는 각 요소간의 연결만 변경해주면 되기 때문에 처리속도가 상당히 빠르다. 반면에 ArrayList는 각 요소들을 재배치하여 추가할 공간을 확보하거나 빈 공간을 채워야 하기 때문에 처리 속도가 늦다. 

- 원하는 인덱스의 값을 얻어오고자 할 때 ArrayList가 LinkedList보다 빠르다.
배열은 각 요소들이 연속적으로 메모리상에 존재하기 때문에 배열의 첫 주소를 알고 있으면 인덱스의 주소를 계산하여 접근할 수 있다. 
LinkedList는 불연속적으로 위치한 각 요소들을 Node로 연결한 형태이기 때문에 인덱스의 원소를 알기 위해서는 순차적으로 데이터를 돌아야 한다. 
컬렉션	읽기(접근시간)	추가/삭제	
ArrayList	빠르다	느리다	순차적인 추가/삭제는 더 빠름,  비효율적인 메모리 사용
LinkedList	느리다	빠르다	데이터가 많을 수록 접근성이 떨어짐![](https://images.velog.io/images/hweyoung/post/cc082e83-74cc-403f-9791-90931215a6e7/image.png)

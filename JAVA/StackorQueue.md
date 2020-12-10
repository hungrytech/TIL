# Stack 과 Queue
> 자바의 정석 Stack 과 Queue 학습 
> Stack
> Queue

## Stack
* 스택은 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 LIFO(Last In First Out)구조로 되어있다.
![screensh](https://res.cloudinary.com/practicaldev/image/fetch/s--agJOq1EO--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/ne9kc5zo8kqmvh34c3zu.jpg)

* 스택에 0, 1, 2의 순서로 데이터를 넣었다면 꺼낼 때는 2, 1, 0의 순서로 꺼내게 된다.
* Java에서는 ArrayList와 같은 배열기반의 컬렉션 클래스가 적합하다.

 ```java
  class StackQueueEx {
    Public static void main(String [] args) {
      Stack st = new Stack();
      st.push("0");
      st.push("1");
      st.push("2");
      
      while (!st.empty()) {
        System.out.println(st.pop());
      }
    }          
  }
  ```
* 실행시키면 2, 1, 0 순으로 나오게 된다. 
  
## Queue
* 큐는 처음의 저장한 데이터를 가장 먼저 꺼내게 되는 FIFO(First In First Out)구조로 되어 있다.
![screensh](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F190E0A214CFF935221F08E)

* 스택에 0, 1, 2의 순서로 데이터를 넣었다면 꺼낼 때는 0, 1, 2의 순서로 꺼내게 된다.
* ArrayList는 큐에서는 데이터를 꺼낼때 항상 첫 번째 저장된 데이터를 삭제하므로, 빈 공간을 채우기 위해 데이터 복사가 발생하여 비효율적이다. 
* 따라서 큐는 데이터 추가/삭제가 쉬운 LinkedList로 구현하는 것이 더 적합하다.

```java
  class StackQueueEx {
    Public static void main(String [] args) {
      Queue q = new LinkedList();
      q.offer("0");
      q.offer("1");
      q.offer("2");
      
      while (!q.isempty()) {
        System.out.println(q.poll());
      }
    }          
  }
  ```
  
* 실행시키면 0, 1, 2 순으로 나오게 된다.

* 자바에서는 스택을 Stack클래스로 구현하고 제공한다. 
* 큐는 Queue인터페이스로만 정의해 놓았을 뿐 별도 클래스를 제공하지 않고 있다.
 * 대신 Queue인터페이스를 구현한 클래스들이 있어서 이 들 중의 하나를 선택해서 사용하면 된다.
 

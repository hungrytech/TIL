# 자바의 정석 Iterator과 Arrays
>
> Iterator
>
> Arrays

* * *
## Iterator

컬렉션에 저장된 각 요소에 접근하는 기능을 가진 Iterator인터페이스를 정의하고, Collection인터페이스에는 'Iterator(Iterator를 구현한 클래스의 인스턴스)'를 반환하는 iterator()를 정의하고 있다.

```java
public interface Iterator{
  boolean hasNext();
  Object next();
  void remove();
}
public interface Collection{
  ...
  public Iterator iterator();
  ...
}
```

iterator()sms Collection인터페이스에 정의된 메서드이므로 Collection인터페이스의 자손인 List와 Set에도 포함되어있다.
그래서 List나 Set인터페이스를 구현하는 컬렉션은 Iterator()가 각 컬렉션의 특징의 알맞게 작성되어 있다.
컬렉션 클래스에 대해 iterator()를 호출하여 Iterator를 얻은 다음 반복문, 주로 while문을 사용해서 컬렉션 클래스의 요소들을 읽어 올 수 있다.

* Iterator의 메소드
  * boolean hasNext() 읽어 올 요소가 남아있는지 확인한다. 있으면 true 없으면 false를 반환한다.
  * Object next() 다음 요소를 읽어 온다. next()를 호출하기전에 hasNext()를 호출하여 읽어올 요소가 있는지 확인하는 것이 안전하다.
  * void remove() next()로 읽어 온 요소를 삭제한다. next()를 호출한 다음에 renmove()를 호출해야한다. (선택적 기능)
  

(선택적 기능) 인 remove() 메서드는 구현하지 않아도 괜찮다. 그렇다해도 인터페이스로부터 상속받은 메서드는 추상메서드라 메서드의 몸통(body)을 반드시 만들어 주어야 하므로 처리한다

```java
public void remove() {
  throw new UnsupportedOpreationException();
}
```

* Iterator의 remove()는 단독으로 쓰일 수 없고, next()와 같이 써야한다.
  * 특정위치의 요소를 삭제하는것이 아닌 next()로 읽어온 것을 삭제한다.
  
Map인터페이스를 구현한 컬렉션 클래스는 키(Key)와 값(value)을 쌍(pair)으로 저장하고 있기 때문에 iterator()를 직접 호출할 수 없고, 그 대신 keySet()이나 entry()과 같은 메서드를 통해서 
키와 값을 각각 따로 Set의 형태로 얻어 온 후에 다시 iterator()를 호출해야 Iterator를 얻을 수 있다.

```java
Map map = new HashMap();
Iterator it = map.entrySet().iterator();
```

## Arrays

Arrays클래스에는 배열을 다루는데 유용한 메서드가 정의되어 있다.

* Arrays에 정의된 메서드는 모두 Static메서드이다.

```java
static String toString(boolean[] a)
static String toString(byte[] a)
static String toString(char[] a)
static String toString(short[] a)
static String toString(int[] a)
static String toString(long[] a)
static String toString(float[] a)
static String toString(double[] a)
static String toString(Object[] a)
```

### 배열의 복사 -copyOf(), copyOfRange()

* copyOf()는 배열 전체를 복사해서 새로운 배열을 만들어 반환한다.
* copyOfRange()는 배열의 일부를 복사해서 새로운 배열을 만들어 반환한다.

```java
int[] arr = {0,1,2,3,4};
int[] arr2 = Arrays.copyOf(arr, arr.length); // arr2 = {0,1,2,3,4}
int[] arr3 = Arrays.copyOf(arr, 3); // arr3 = {0,1,2}
int[] arr4 = Arrays.copyOfRange(arr, 2, 4); // arr4 = {2,3}
```

### 배열 채우기 -fill(), setAll()

* fill()은 배열의 모든 요소를 지정된 값으로 채운다.
* setAll()은 배열을 채우는데 사용할 함수형 인터페이스를 구현한 객체를 매개변수로 지정하던가 아니면 람다식을 지정해야한다.

```java
int[] arr = new int[5];
Arrays.fill(arr, 9); // arr = {9,9,9,9,9}
Arrays.setAll(arr, () -> (int) (Math.random()*5)+1); // arr = {1,5,4,1,2}
```

### 배열의 정렬과 검색 -sort(), binarySearch()

* sort()는 배열을 정렬할 때 사용한다.
* binarySearch() 배열에서 지정된 값이 저장된 위치(index)를 찾아서 반환하는데, 반드시 배열이 정렬된 상태이어야 올바른 결과를 얻는다.
  * 만일 일치하는 요소들이 여러 개 있다면, 이 중에서 어떤 것의 위치가 반환될지는 알 수 없다.

```java
int[] arr = {3,1,0,2,4};
int idx = Arrays.binarySearch(arr, 2); // 잘못된 결과가 나온다

Arrays.sort(arr); // 배열 arr를 정렬한다.
System.out.println(Arrays.toString(arr)); // [0,1,2,3,4]
int idx = Arrays.binarySearch(arr, 2); // idx = 2 올바른 결과가 나온다
```

* 배열의 첫번째 요소부터 순서대로 하나씩 검색하는 것을 '순차 검색(linear search)'이라고 한다.
이 검색 방법은 정렬되어 있을 필요는 없지만 배열요소를 하나씩 비교하기 때문에 시간이 많이 걸린다.

* 이진 검색(bineary search)은 배열의 검색할 범위를 반복적으로 절반씩 줄여가면서 검색한다.
검색속도가 상당히 빠르다. 따라서 큰 배열의 검색에 유리하다

### 배열의 비교와 출력 -equals(), toString()

```java
int[] arr = {0,1,2,3,4};
int[][] arr2D = {{11,12}, {21, 22}};

System.out.println(Arrays.toString(arr)); // [0,1,2,3,4]
System.out.println(Arrays.deepToString(arr2D)); // [[11,12],[21,22]]
```
* 2차원, 3차원 이상의 배열에서는 deepToString()을 사용해야 한다.

```java
String[][] str2D = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};
String[][] str2D2 = new String[][]{{"aaa", "bbb"}, {"AAA", "BBB"}};

System.out.println(Arrays.equals(str2D, str2D2)); // false
System.out.println(Arrays.deepEquals(str2D, str2D2)); // ture
```

* 2차원 String배열을 equals()로 비교하면 저장된 내용이 같아도 false를 결과로 얻는다.
문자열을 비교하는 것이 아니라 '배열에 저장된 배열의 주소'를 비교하게 된다.

* 다차원이상의 배열의 비교는 deepEquals()를 써야한다.

### 배열을 List로 반환 - asList(Object.. a)

* asList()는 배열을 List에 담하서 반환한다. 
* 매개변수의 타입이 가변인수라서 배열 생성없이 저장할 요소들만 나열하는 것도 가능하다.

```java
List list = Arrays.asList(new Integer[]{1,2,3,4,5}); // list = [1,2,3,4,5]
List list = Arrays.asList(1,2,3,4,5); // list = [1,2,3,4,5]
list.add(6); // UnsupportedOpreationException 예외 발생
```

* asList()가 반환한 List의 크기를 변경할 수 없다.
* 추가 삭제가 불가능하다.
* 저장된 내용은 변경가능하다.


 

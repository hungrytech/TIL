# 자바의 정석 Comparator와 Comparable

Arrays.sort()를 호출을 하면 컴퓨터가 알아서 배열을 정렬하는것이 아니라 Character클래스의 Comparable의 구현에 의해 정렬되는 것이다.

* Comparator와 Comparable은 모두 인터페이스로 컬렉션을 정렬하는데 필요한 메서드를 정의하고 있다.

```java
public interface Comparator {
  int compare(Object o1, Object o2);
  boolean equals(Object obj);
}
public interface Comparable {
  public int compareTo(Object o);
}
```

* compare()와 compareTo()는 선언형태와 이름이 약간 다를 뿐 두 객체를 비교한다는 같은 기능을 목적으로 고안되었다.
  * compareTo()의 반환값은 int이지만 실제로는 비교하는 두 객체가 같으면 0, 비교하는 값보다 작으면 음수, 크면 양수를 반환하도록 구현해야 한다.
* equals메서드는 모든 클래스가 가지고 있는 공통적인 메서드이지만, Comparator를 구현하는 클래스는 오버라이딩이 필요할 수도 있다는 것을 알리기 위해서 정의한 것이다.
  * compare(Object o1, Object o2)만 구현하면 된다.

```java
public final class Interger extends Number implements Comparable {
  ...
  public int compareTo(Objcet o) {
    return compareTo((Integer)o);
  }
  public int compareTo(Integer anotherInteger) {
    int thisVal = this.value;
    int anotherVal = anotherInteger.value;

    //비교하는 값이 크면 -1, 같으면 0, 작으면 1을 반환한다.
    return (thisVal<anotherVal ? -1 : (thisVal==anotherVal ? 0 : 1)); 
  }
  ...
}
```

* Comparable의 compareTo(Object o)를 구현해 놓았다.
  * 두 Integer객체에 저장된 int값(value)을 비교해서 같으면 0, 크면 -1, 작으면 1을 반환하는 것을 알 수 있다.
  
Comparable을 구현한 클래스들이 기본적으로 오름차순으로 정렬되어 있지만, 내림차순으로 정렬한다던가 아니면 다른 기준에 의해서 정렬되도록 하고 싶을때 
Comparator를 구현해서 정렬기준을 제공할 수 있다.

* Comparable 기본 정렬기준을 구현하는데 사용.
* Comparator 기본 정렬기준 외에 다른 기준으로 정렬하고자할 때 사용

```java
String[] strArr = {"Dog","cat",  "lion", "tiger"};

Arrays.sort(strArr, String.CASE_INSENSITIVE_ORDER); // 대소문자 구분안함
System.out.println("strArr=" + Arrays.toString(strArr)); // strArr = [cat, Dog, lion, tiger]

```




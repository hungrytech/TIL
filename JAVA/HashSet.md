# 자바의 정석 HashSet

* Set인터페이스의 특징대로 증복된 요소를 저장하지 않는다.
* HashSet에 이미 저장되어 있는 요소와 증복된 요소를 추가하고자 하면 이 메서드들은 false를 반환함으로써 증복된 요소이기에 추가에 실패했다는 것을 알린다.
* HashSet의 특징을 이용하면, 컬렉션 내의 증복 요소들을 쉽게 제거할 수 있다.
* HashSet은 저장순서를 유지하지 않으므로 저장순서를 유지하고자 한다면 LinkedHashSet을 사용해야 한다.

* * *
* HashSet()
  * HashSet객체를 생성한다.
* HashSet(Colleciton c)
  * 주어진 컬렉션을 포함하는 HashSet객체를 생성한다.
* boolean add(Object o)
  * 새로운 객체를 저장한다.
* boolean addAll(Collection c)
  * 주어진 컬렉션에 저장된 모든 객체들을 추가한다. (합집합)
* boolean removeAll(Collection c)
  * 주어진 컬렉션에 저장된 모든 객체와 동일한 것들을 HashSet에서 모두 삭제한다. (차집합)
* boolean retainAll(Collection c)
  * 주어진 컬렉션에 저장된 객체와 동일한 것만 남기고 삭제한다. (교집합)
* * * 

```java
Object[] objArr = {"1", new Integer(1), "2", "2", "3", "3", "4", "4"};
Set set = new HashSet();

for (int i=0; i < objArr.length; i++) {
  set.add(objArr[i]); // HashSet에 objArr의 요소들을 저장한다.
}
System.out.println(set); // [1, 1, 2, 3, 4]
```

* 증복된 값은 저장되지 않았다.
* 1이 두번 출력된 이유는 하나는 String인스턴스이고 다른 하나는 Integer인스턴스로 서로 다른 객체이므로 증복으로 간주하지 않는다.
* Set을 구현한 컬렉션 클래스는 List를 구현한 컬렉션 클래스와 달리 순서를 유지하지 않기 때문에 저장한 순서와 다를 수 있다.
* 중복제거와 동시에 저장한 순서를 유지하고자 한다면 HashSet대신 LinkedHashSet을 사용해야 한다.
* * *

```java
class Person {
  String name;
  int age;
  Person (String name, int age) {
    this.name = name;
    this.age = age;
  }
  // equals와 hashCode를 오버라이딩 해주어야 한다.
  public boolean equals(Object obj) {
    if(!(obj instanceof Person)) return false;
    Person p = (Person)Obj;
    return this.name.equals(p.name) && this.age == p.age; // 나자신(this)의 이름과 나이를 p와 비교
  }
  
  public int hashCode() {
    return Objects.hash(name, age);
  }
```

HasgSet의 add메서드는 새로운 요소를 추가하기 전에 기존에 저장된 요소와 같은 것인지 판별하기 위해 추가하려는 요소의 equals()와 hashCode()를 호출하기 때문에 
equals()와 hashCode()를 목적에 맞게 오버라이딩해야 한다.
  


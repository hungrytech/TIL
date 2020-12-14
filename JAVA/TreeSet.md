# 자바의 정석 TreeSet

* TreeSet은 이진 검색 트리(binary search tree)라는 자료구조의 형태로 데이터를 저장하는 클래스이다.
* Set인터페이스로 구현했으므로 증복데이터의 저장을 허용하지 않는다.
* 정렬된 위치에 저장하므로 저장순서를 유지하지도 않는다.

이진트리(bineary tree)는 여러개의 노드(node)가 서로 연결된 구조이고 각 노드에 최대 2개의 노드를 연결할 수 있으며 
루트(root)라고 불리는 하나의 노드에서부터 시작해서 계속 확장해 나갈 수 있다.

![](https://www.google.com/url?sa=i&url=https%3A%2F%2Fko.wikipedia.org%2Fwiki%2F%25EC%259D%25B4%25EC%25A7%2584_%25ED%258A%25B8%25EB%25A6%25AC&psig=AOvVaw2nAfdydhXPia9Oi4-IHoWU&ust=1608040549817000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCLjIzoDQze0CFQAAAAAdAAAAABAD)

* 위 아래로 연결된 두 노드를 '부모 - 자식관계'에 있다고 한다.
* 하나의 부모 노드는 최대 두개의 자식 노드와 연결될 수 있다.

```java
class TreeNode {
  TreeNode left;   // 왼쪽 자식노드
  Object element;  // 객체를 저장하기 위한 참조변수
  TreeNode right;  // 오른쪽 자식노드
```

* 첫번째로 저장되는 값은 루트가 된다.
* 두번째 값은 트리의 루트부터 시작해서 값의 크기를 비교하면서 트리를 따라 내려간다.
>
* 부모노드의 왼쪽에는 부모노드의 값보다 작은 값의 자식노드를 둔다.
* 부모노드의 오른쪽에는 부모노드의 값보다 큰 값의 자식노드를 둔다.
>
>
* 값을 비교하기 위해서는 TreeSet에 저장되는 객체가 Comparable을 구현하거나,  TreeSet에게 Comparator를 제공해서 두 객체를 비교할 방법을 알려줘야 한다.
  * 그렇지 않으면, TreeSet에 객체를 저장할 때 예외가 발생한다.
* 왼쪽 마지막 값에서부터 오른쪽 값까지의 값을  '왼쪽노드 -> 부모 노드 -> 오른쪽 노드' 순으로 읽어오면 오름차순으로 정렬된 순서를 얻을 수 있다.
* TreeSet은 정렬된 상태를 유지하기 때문에 단일 값 검색과 범위검색(range search)이 매우 빠르다.
* 링크드 리스트보다 데이터의 추가/삭제시간은 더걸리나,  배열이나 링크드 리스트에 비해 검색과 정렬기능이 더 뛰어나다.
>
>
* TreeSet() : 기본생성자
* TreeSet(Collection c) : 주어진 컬렉션을 저장하는 TreeSet을 생성
* TreeSet(Comparator comp) : 주어진 정렬조건으로 정렬하는 TreeSet을 생성
* SortedSet tailSet(Object fromElement) : 지정된 객체보다 큰 값의 객체들을 반환한다.
* SortedSet headSet(Object toElement) : 지정된 객체보다 작은 값의 객체들을 반환한다.
* SortedSet subSet(Object fromElement, Object toElement) : 범위검색 (fromElement와 toElement사이)의 결과를 반환한다.  끝 범위인 toElement는 범위에 포함되지 않는다.

```java
import java.util.*;

class TreeSetEx2 {
  public static void main(String[] args) {
    TreeSet set = new TreeSet();
    int[] score = {80, 95, 50, 35, 45, 65, 10, 100};
    
    for(int i=0; i < score.length; i++) 
      set.add(new Integer(score[i]));
     System.out.println(set.headSet(new Integer(50))); // 50보다 작은 값 : [10, 35, 45]
     System.out.println(set.tailSet(new Integer(50))); // 50보다 큰 값 : [50, 65, 80, 95, 100]
```
  

### Heap
  - 비선형 자료구조
  - Heap은 완전 이진 트리 형태(마지막 레벨을 제외하고 노드들이 모두 채워져있는 트리)
  - 중복 값을 허용하고 반 정렬 상태
  - 최소값 또는 최대값을 빠르게 찾아내는데 유용한 자료구조(최소 힙, 최대 힙)
  - 알고리즘 위상정렬, 최대 값 뽑아내기 등 문제에 사용
  - 여러개의 값을 비교하여 최대, 최소를 구하라는 요구가 주어질 때 Comparable을 상속 받은 클래스를 구현하고 PriorityQueue 제너릭 타입에 넣어서 사용
  - 최소 힙
    - 부모 노드의 키가 자식 노드의 키보다 작거나 같은 형태
  - 최대 힙
    - 부모 노드의 키가 자식 노드의 키보다 크거나 같은 형태
  - ArrayList를 이용한 최소, 최대 힙 구현
  ```java
    // 
    class MinHeap {
      ArrayList<Integer> heap;

      public MinHeap() {
          this.heap = new ArrayList<>();
          this.heap.add(0);
      }

      public void insert(int data) {
          this.heap.add(data);

          int cur = heap.size() - 1;
          while (cur > 1 && heap.get(cur / 2) > heap.get(cur)) {
              int parent = heap.get(cur / 2);
              heap.set(cur / 2, data);
              heap.set(cur, parent);
              cur /= 2;
          }
      }

      public Integer delete() {
          if (this.heap.size() == 1) {
              System.out.println("Heap is empty");
              return null;
          }

          int target = heap.get(1);
          heap.set(1, heap.get(heap.size() - 1));
          heap.remove(heap.size() - 1);

          int cur = 1;
          while (true) {
              int leftIdx = cur * 2;
              int rightIdx = cur * 2 + 1;
              int targetIdx = -1;

              if (rightIdx < heap.size()) {
                  targetIdx = heap.get(leftIdx) < heap.get(rightIdx) ? leftIdx : rightIdx;
              } else if (leftIdx < heap.size()) {
                  targetIdx = leftIdx;
              } else {
                  break;
              }

              if (heap.get(cur) < heap.get(targetIdx)) {
                  break;
              } else {
                  int parent = heap.get(cur);
                  heap.set(cur, heap.get(targetIdx));
                  heap.set(targetIdx, parent);

                  cur = targetIdx;
              }
          }

          return target;
      }

      public void printTree() {
          for (int i = 1; i < this.heap.size(); i++) {
              System.out.print(this.heap.get(i) + " ");
          }
          System.out.println();
      }
    }
  
    // 
    class MaxHeap {
      ArrayList<Integer> heap;

      public MaxHeap() {
          this.heap = new ArrayList<>();
          this.heap.add(0);
      }

      public void insert(int data) {
          this.heap.add(data);

          int cur = heap.size() - 1;
          while (cur > 1 && heap.get(cur / 2) < heap.get(cur)) {
              int parent = heap.get(cur / 2);
              heap.set(cur / 2, data);
              heap.set(cur, parent);
              cur /= 2;
          }
      }

      public Integer delete() {
          if (this.heap.size() == 1) {
              System.out.println("Heap is empty");
              return null;
          }

          int target = heap.get(1);
          heap.set(1, heap.get(heap.size() - 1));
          heap.remove(heap.size() - 1);

          int cur = 1;
          while (true) {
              int leftIdx = cur * 2;
              int rightIdx = cur * 2 + 1;
              int targetIdx = -1;

              if (rightIdx < heap.size()) {
                  targetIdx = heap.get(leftIdx) > heap.get(rightIdx) ? leftIdx : rightIdx;
              } else if (leftIdx < heap.size()) {
                  targetIdx = leftIdx;
              } else {
                  break;
              }

              if (heap.get(cur) > heap.get(targetIdx)) {
                  break;
              } else {
                  int parent = heap.get(cur);
                  heap.set(cur, heap.get(targetIdx));
                  heap.set(targetIdx, parent);

                  cur = targetIdx;
              }
          }

          return target;
      }

      public void printTree() {
          for (int i = 1; i < this.heap.size(); i++) {
              System.out.print(this.heap.get(i) + " ");
          }
          System.out.println();
      }
  }
  ```
  
  - PriorityQueue를 이용한 최소, 최대 힙
  ```java
    import java.util.Collections;
    import java.util.PriorityQueue;

    public class Heap {

        public static void main(String[] args) {
            PriorityQueue<Integer> minHeap = new PriorityQueue<>();
            minHeap.add(30);
            minHeap.add(10);
            minHeap.add(50);
            minHeap.add(1);

            while (!minHeap.isEmpty()) {
                System.out.print(minHeap.poll() + " ");
            }
            System.out.println();

            PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
            maxHeap.add(30);
            maxHeap.add(10);
            maxHeap.add(50);
            maxHeap.add(1);

            while (!maxHeap.isEmpty()) {
                System.out.print(maxHeap.poll() + " ");
            }
            System.out.println();
        }
    }
  ```
  - PriorityQueue를 이용한 객체 정렬
  ```java
      import java.util.PriorityQueue;

      class Person implements Comparable<Person> {
        String name;
        int age;

        public Person(String name, int age) {
            this.name = name;
            this.age = age;
        }

        @Override
        public int compareTo(Person o) {
            // 1 : 변경 안 함
            // -1 : 변경
            // 새롭게 추가하는(this) 데이터가 원래 데이터(o)보다 더 적을 때 변경(적은 값이 올라감, 오름차순)
            return this.age <= o.age ? -1 : 1;

            // 내림차순
            return o.age <= this.age ? -1: 1;
        }
    }

    public class Practice1 {
        public static void solution(String[] name, int[] age) {
            PriorityQueue<Person> persons = new PriorityQueue<>();
            for (int i = 0; i < name.length; i++) {
                Person person = new Person(name[i], age[i]);
                persons.add(person);
            }

            while (!persons.isEmpty()) {
                Person person = persons.poll();
                System.out.println(person.name + "  " + person.age);
            }
        }

        public static void main(String[] args) {
            String[] name = {"A", "B", "C", "D", "E"};
            int[] age = {30, 20, 45, 62, 35};

            solution(name, age);
            System.out.println("===========");
            
            // 람다식으로 객체에 Comparable을 구현 하지 않고 사용 가능
            PriorityQueue<Person> person2 = new PriorityQueue<>((Person p1, Person p2) -> (p1.age <= p2.age ? -1 : 1));

            for (int i = 0; i < name.length; i++) {
                Person person = new Person(name[i], age[i]);
                person2.add(person);
            }

            while (!person2.isEmpty()) {
                Person person = person2.poll();
                System.out.println(person.name + "  " + person.age);
            }
        }
    }
  ```

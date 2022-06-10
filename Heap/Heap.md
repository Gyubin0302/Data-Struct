### Heap
  - 비선형 자료구조
  - Heap은 완전 이진 트리 형태(마지막 레벨을 제외하고 노드들이 모두 채워져있는 트리)
  - 중복 값을 허용하고 반 정렬 상태
  - 최소값 또는 최대값을 빠르게 찾아내는데 유용한 자료구조(최소 힙, 최대 힙)
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

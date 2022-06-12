### Trie
  - 문자열을 저장하고 빠르게 탐색하기 위한 트리 형태의 자료구조
  - 정렬된 트리 구조
  - 루트 노드는 비어있고 루트의 자식 노드부터 문자열의 첫 단어가 저장
  - 문자열 저장을 위한 메모리가 필요하지만 탐색이 빠름. 길이가 N인 문자열 탐색의 시간 복잡도O(N)
  - 생성 복잡도는 O(MN) M은 문자열 개수
  - Map을 사용하여 구현
  ```java
    class Node {
      HashMap<Character, Node> child;
      boolean isTerminal;
      
      public Node() {
        this.child = new HashMap<>();
        this.isTerminal = false;
      }
    }
    
    class Trie {
      Node root;
      
      public Trie() {
        this.root = new Node();
      }
      
      public void insert(String str) {
        Node cur = this.root;
        
        for (int i = 0; i < str.length(); i++) {
          char c = str.charAt(i);
          
          // key 값이 존재하는 경우 Map의 Value를 반환하고 존재하지 않은 경우 Key, Value를 put
          cur = cur.child.computeIfAbsent(c, key -> new Node());
        }
        cur.isTerminal = true;
      }
      
      public boolean search(String str) {
        Node cur = this.root;
        
        for (int i = 0; i < str.length(); i++) {
          char c = str.charAt(i);
          
          cur = cur.child.getOrDefault(c, null);
          
          if (cur == null) {
            return false;
          }
        }
        
        return cur.isTerminal;
      }
      
      public void delete(String str) {
        boolean ret = this.delete(this.root, str, 0);
        if (ret) {
          System.out.println(str + " delete complete");
        } else {
          System.out.println(str + " delete not complete");
        }
      }
      
      public boolean delete(Node node, String str, int idx) {
        char c = str.charAt(idx);
        
        if(!node.child.containsKey(c)) {
          return false;
        }
        
        Node cur = node.child.get(c);
        idx++;
        if (idx == str.length()) {
          if (!cur.isTerminal) {
            return false;
          }
          
          cur.isTerminal = true;
          
          if (cur.child.isEmpty()) {
            node.child.remove(c);
          }
        } else {
          if (!this.delete(cur, str, idx)) {
            return false;
          }
          
          if (!cur.isTerminal && cur.child.isEmpty()) {
            node.child.remove(c);
          }
        }
        
        return true;
      }
    }
  ```

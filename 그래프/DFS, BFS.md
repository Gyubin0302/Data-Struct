### DFS(Depth First Search)
  - 그래프 탐색의 한 종류
  - 깊이 우선 탐색이라고 부름
  - 루트 노드나 임의의 노드에서 시작하여 최대로 진입할 수 있는 깊이까지 탐색한 후 돌아와 다른 노드로 탐색하는 방식
  - Stack or recursion function을 사용하여 데이터를 탐색
  - 장점
    - 현 경로상의 노드들만 기억하면 되므로 저장공간 수요가 비교적 적음
    - 목표 노드가 깊은 단계에 있을 경우 해를 빨리 구할 수 있음
    - BFS에 비해 저장공간의 필요성이 적음. 백트래킹 해야하는 노드들만 저장하면 됨
    - 찾아야하는 노드가 깊은 단계에 있을 수록 그 노드가 좌측에 있을 수록 BFS보다 유리
  - 단점
    - 해가 없는 경로가 깊을 경우 탐색시간이 오래 걸리 수 있음
    - 얻어진 해가 최단 경로가 된다는 보장이 없음
  ```java
    public static void recursionDfs(int x) {
        visited[x] = true;
        answer[x] = ++idx;
        for (int i = 0; i < graph.get(x).size(); i++) {
            int y = graph.get(x).get(i);
            if(!visited[y]) {
                dfs(y);
            }
        }
    }
  ```
  
### BFS(Breadth First Search)
  - 그래프 탐색의 한 종류
  - 너비 우선 탐색이라고 부름
  - 루트 노드나 임의의 노드에서 시작하여 인접한 노드를 먼저 모두 확인 후 다음 깊이를 탐색
  - Queue를 사용하여 데이터를 탐색
  - 장점
    - 너비를 우선으로 탐색하기 때문에 답이 되는 경로가 여러개인 경우에도 최단 경로임을 보장
    - 최단 경로가 존재한다면, 어느 한 경로가 무한히 깊어진다 해도 최단 경로를 반드시 찾을 수 있음
    - 노드 수가 적고 깊이가 얕은 해가 존재 할 때 유리
  - 단점
    - 재귀함수를 사용하는 DFS와 달리 Queue를 이용해 다음 탐색 할 노드들을 저장하기 때문에 노드의 수가 많을 수록 필요 없는 노드들까지 저장해야 하기 때문에 더 큰 저장공간 필요
    - 노드의 수가 늘어나면 탐색해야하는 노드가 많아지기 때문에 비효율적
  ```java
   public static void bfs(int x) {
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(x);
        visited[x] = true;
        while (!queue.isEmpty()) {
            int n = queue.poll();
            answer[n] = ++idx;
            for (int i = 0; i < graph.get(n).size(); i++) {
                int m = graph.get(n).get(i);
                if(!visited[m]) {
                    queue.offer(m);
                    visited[m] = true;
                }
            }
        }
    }
  ```
  

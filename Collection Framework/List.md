#### List  
  - List 자료형에는 ArrayList, LinkedList, Vector가 있다.  
  - 애플리케이션 새발 업무에 List collection이 많이 쓰이고 특히 ArrayList가 많이 사용된다.  
  - 객체를 일렬로 늘어놓은 구조이다. add, contain, get, size, remove, clear 메서드가 선언 되어 있다.  
  
#### ArrayList  
  - List collection 인터페이스를 구현한 클래스이다.  
  - 일반 배열과 인덱스로 객체를 관리한다는 점은 동일하지만 크기를 동적으로 늘릴 수 있는 차이가 있다.  
  - 제네릭스는 클래스형만 사용 가능  
  - 예제  
  ``` java  
  List<Integer> nums = new ArrayList<Integer>();
  nums.add(1); // 0번 배열에 값 추가  
  nums.add(2); // 1번 배열에 값 추가  
  nums.add(2, 3);  // 2번 배열에 값 추가
  System.out.println(nums.size()); // 현재 배열 사이즈 출력  
  ```  
 #### Vector  
  - Vector class는 예전의 자바에서 제공했던 레거시 클래스이다.   
  - 레거시 클래스란 Collections 프레임워크가 포함되어 있지 않던 초기 자바 버전에서 정의한 인터페이스이다.  
  - 현재는 재구성 및 설계되어서 현재의 Collections 프레임워크와 완벽하게 호환이된다.  
  - 필요에 따라 크기를 동적으로 조절 가능.  
  - 베열과 마찬가지로 정수 인덱스를 이용하여 배열에 접근가능.  
  - 동기화(Thread Safe)되어있으며 한번에 하나의 Thread만 벡터 메소드에서 호출 가능.  
    
 #### ArrayList와 Vector의 차이  
  - 동기화 : Vector는 동기화된 상태, ArrayList는 동기화가 되지 않은 상태. Vector는 하나의 Thread만 접근 가능하며, ArrayList는 동시에 여러 Thread가 가능  
  - Thread Safe : 스레드안전이란 멀티 스레드 프로그래밍에서 여러 스레드가 동시에 접근이 이루어져도 프로그램 실행에 문제가 없음을 듯함  
  - 성능 : ArrayList가 동기화 되지 않았기 때문에 더 빠르다.  
  - 크기증가 : Vector는 현재 배열의 100%크기, ArrayList는 현재 배열의 50%크기  
  

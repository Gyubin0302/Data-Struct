#### Map  
  - Map 인터페이스는 Collections 인터페이스와는 다른 저장 방식을 가진다.  
  - Map 인터페이스를 구현한 Map Collections 클래스들은 Key, Value값을 하나의 쌍으로 저장하는 방식을 사용한다.  
  - Key는 Value를 찾기 위한 이름의 역할을 한다.  
  - 요소의 저장 순서가 없다.  Key는 중복을 허용하고, Value는 중복이 허용되지 않는다.  
  
#### HashMap  
  - Map Collections에서 가장 많이 사용되는 클래스이다.  
  - HashMap은 Map을 구현한다. Key와 Value를 묶어 하나의 entry로 저장한다는 특징을 갖는다.  
  - Hash alrgorithm을 사용하여 많은 양의 데이터를 검색하는데 검색 속도가 매우 빠르다.  
  - 중복된 Key로는 값을 저장할 수 없다. Value에 null 값도 사용 가능하다.  
  - multi thread에서는 HashTable을 사용한다.  
  
  
#### HashTable  
  - HashMap 클래스와 같은 동작을 하는 클래스이다.  
  - HashTable 클래스는 HashMap 클래스와 마찬가지로 Map 인터페이스를 상속 받는다.  
  
#### 예제  
``` java  
package com.bit.ex;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class Hash {

	public static void main(String[] args) {
		
		Map<String, Double> productPrice = new HashMap<>();
		
		// put으로 Key와 Value추가 
		productPrice.put("Rice", 6.9);
		productPrice.put("Flour", 3.9);
		productPrice.put("Sugar", 4.9);
		productPrice.put("Milk", 3.9);
		productPrice.put("Egg", 1.9);
		
		// Key값으로 Value 찾기
		System.out.println(productPrice.get("Rice"));
		System.out.println(productPrice.get("Flour"));
		System.out.println(productPrice.get("Sugar"));
		System.out.println(productPrice.get("Milk"));
		System.out.println(productPrice.get("Egg"));
		System.out.println();
		
		// Set으로 모든 key 출력
		Set<String> keys = productPrice.keySet();
		keys.forEach(key -> System.out.println(key));
		System.out.println();
		
		// 모든 Value 출력(Lamda expression)
		Collection<Double> vals = productPrice.values();
		vals.forEach(val -> System.out.println(val));
		System.out.println();
		
		
		// 모든 Key, Value 출력(Lamda expression)
		Set<Map.Entry<String, Double>> entries = productPrice.entrySet();
		productPrice.forEach((key, value) ->{
			System.out.print("key : " + key + " " );
			System.out.println("value : " + value);
		});

	}

}
```  
![image](https://user-images.githubusercontent.com/67041069/87508927-6a19bb80-c6ab-11ea-8d13-05fddaba210b.png)  

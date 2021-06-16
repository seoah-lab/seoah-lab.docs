---
title: Java Map to Iterate
weight: 1
---

# Java Map to Iterate

HashMap 의 key 와 value를 확인할때 활용할 수 있는 방법은 다음과 같다.

```java 
import java.util.Map;
import java.util.HashMap;

class Iteration {
	public static void main(String[] arg) {
		Map<String,Integer> map = new HashMap<>();
	
		// enter name/url pair
		map.put("sogmy", 1);
		map.put("hyunjin", 2);
		map.put("suji", 3);
		map.put("young", 4);
		map.put("ki", 5);

        Iterator<Map.Entry<String, Interger>> itr = map.entrySet().iterator();
         
        while(itr.hasNext()) {
             Map.Entry<String, Interger> entry = itr.next();
             System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
        }

		for (Map.Entry<String,Interger> entry : map.entrySet()) {
            System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
        }
			

        for (String name : map.keySet()) {
            System.out.println("key: " + name);
        }
        
        
        for (String url : map.values()) {
            System.out.println("value: " + url);
        }

        map.forEach((k,v) -> System.out.println("Key = " + k + ", Value = " + v));
    }
}

```
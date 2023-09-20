---
title: Java Map Sort by key and value
---

# Java Map Sort by key and value

### Map to List 를 활용

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.stream.Collectors;

String[] array = new String[]{"sun", "bed", "car"};
Map<Integer, String> map = new HashMap<>();
map.put(2, array[2]);
map.put(0, array[0]);
map.put(1, array[1]);

// key sort
List<Integer> keyList = new ArrayList<>(map.keySet());
keyList.sort(Comparator.naturalOrder()); // 오름 차순
for (Integer key : keyList) {
    System.out.println("Key: " + key);
}

keyList.sort(Comparator.naturalOrder()); // 내림 차순
for (Integer key : keyList) {
    System.out.println("Key: " + key);
}

// entry set sort by value
List<Entry<Integer,String>> entryList = new ArrayList<>(map.entrySet());
entryList.sort(Entry.comparingByValue());
entryList.forEach(System.out::println);

// stream entry set sort by key
List<Map.Entry<Integer, String>> list = map.entrySet().stream()
    .sorted(Map.Entry.comparingByKey())
    .collect(Collectors.toList());

list.forEach(System.out::println);

```


---
참고  
https://www.delftstack.com/ko/howto/java/how-to-sort-a-map-by-value-in-java/
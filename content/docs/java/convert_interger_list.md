--- 
weight: 1
---
# Convert Integer List to Int Array in Java

List 의 toArray() 메서드는 Object 타입을 지원한다.
즉 int[] 배열은 지원하지 않는다.

### ArrayList toArray()

```java
public Object[] toArray()
           or
public <T> T[] toArray(T[] a)

import java.io.*;
import java.util.List;
import java.util.ArrayList;
  
class Main {
    public static void main(String[] args)
    {
        List<Integer> al = new ArrayList<Integer>();
        al.add(10);
        al.add(20);
        al.add(30);
        al.add(40);
  
        Object[] objects = al.toArray();
  
        // Printing array of objects
        for (Object obj : objects)
            System.out.print(obj + " ");
    }
}
```

### Loop

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args){

        List<Integer> numList = new ArrayList<Integer>();
        numList.add(11);
        numList.add(22);
        numList.add(33);
        numList.add(44);
        numList.add(55);

        int[] numArray = int[numList.size()];

        for (int i = 0; i < numList.size(); i++) {
            numArray[i] = numList.get(i);
            System.out.println(numArray[i]);
        }

    }
}
```

### Stream().mapToInt()


```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args){

        List<Integer> numList = new ArrayList<Integer>();
        numList.add(11);
        numList.add(22);
        numList.add(33);
        numList.add(44);
        numList.add(55);

        int[] numArray = numList.stream().mapToInt(i->i).toArray();

        for (int intValue : numArray) {
            System.out.println(intValue);
        }

    }
}
```
202503041201
Status: #idea
Tags:[[Data Structures (CIS351)]]

Multiple methods may be nearly identical, differing only in their return and parameter types, as shown below.
```java
public static int getElemIndex(String[] array, String elem) {
   for (int i = 0; i < array.length; ++i) {
      if (array[i].equals(elem)) {
         return i;
      }
   }

   return -1; // Element is not in array.
}

public static int getElemIndex(Integer[] array, Integer elem) {
   for (int i = 0; i < array.length; ++i) {
      if (array[i].equals(elem)) {
         return i;
      }
   }

   return -1; // Element is not in array.
}
```

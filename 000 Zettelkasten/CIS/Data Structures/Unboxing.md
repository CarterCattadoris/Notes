202501271204
Status: #idea
Tags:[[Data Types]]

Used for assigning wrapper class variable to primitive type	
```java

Double num1 = 3.14;
Character letter1 = 'A';

double num2 = num1; // Unboxing of Double to double
char letter2 = letter1; // Unboxing of Character to char
```

Pass wrapper class variable to a method with primitive type parameter	
```java
public void setInitial(char letter) {
   // ...
}

Character userInitial = 'Z';
setInitial(userInitial); // Unboxing of userInitial to a char
```

Combine wrapper class and primitive types in expression	
```java

Double currTemp = 95.2;
double tempDiff = 100.0 - currTemp; // Unboxing of currTemp to double

Integer numItems = 11;

if (numItems % 2 == 0) { // Unboxing of numItems to int
   // ...
}
```


---
### References
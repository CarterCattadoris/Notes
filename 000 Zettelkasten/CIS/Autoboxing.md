202501271201
Status: #idea
Tags:[[Data Types]]

used for assigning primitive type to wrapper class variable	

```java
Double floorArea = 20.25; // Autoboxing of 20.25 to a Double
Integer calcResult;

calcResult = 5 / 2; // Autoboxing of expression result to Integer

int num1 = 23;
Integer num2 = num1; // Autoboxing of num1 to Integer
```

Pass primitive type to a method with wrapper class parameter	
```java

public void setRate(Double rate) {
   // ...
}

setRate(50.2); // Autoboxing of 50.2 to Double

double newRate = 97.2;
setRate(newRate); // Autoboxing of newRate to Double
```


---
### References
##Garbage collection


###String Pool
- VM will open a string pool
- we will only have one 'hello' in the heap and two reference variable in stack

```Java
String one = "hello";
String two = "hello";

one.equals(two); // true

String three = new Integer(76).toString();
String four = "76";
String five = new Integer(76).toString().intern();//internized
three.equals(four); // false
// because if string is converted/calculate, then it wont be reused
five.equals(four); // false
```

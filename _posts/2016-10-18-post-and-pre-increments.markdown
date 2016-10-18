---
published: true
title: Post and Pre increments
layout: post
tags: [#Java, #JVM]
---
Study on Pre and Post increment in Java

Interesting Code

```java
public class Sandbox {
    public static void main(String[] args){
        int y = 0;
        y += y++;
        System.out.println(y);


        int z = 0;
        z += ++z;
        System.out.println(z);
    }
}
```
output is 0 and 1

```bytecode
public static void main(java.lang.String[]);
    Code:
       0: iconst_0
       1: istore_1
       2: iload_1
       3: iload_1
       4: iinc          1, 1
       7: iadd
       8: istore_1
       9: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
      12: iload_1
      13: invokevirtual #3                  // Method java/io/PrintStream.println:(I)V
      16: iconst_0
      17: istore_2
      18: iload_2
      19: iinc          2, 1
      22: iload_2
      23: iadd
      24: istore_2
      25: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
      28: iload_2
      29: invokevirtual #3                  // Method java/io/PrintStream.println:(I)V
      32: return
```

Comparing the difference, it is that  line 3,4 and line 18,19 share different orders.

- line 2: load value of y (0)(load first number in addition)
- line 3: load value of y (0)(load second number in addition)
- line 4: increase variable z (but store in other places, as post incremental) 
- line 7: add in 0+0=0
- line 8: store 0 in value y

- line 17: load value of z(0)(load first number in addition)
- line 18: increase variable z
- line 22: load value of z(1)(load second number in addition)
- line 23: add in 0+1=1
- line 24: store 1 in value z

Summary:

- even all the execution is about the same variable, addition will load first operand and then load second operand (from left to right according to precedence, as stack)
- post and pre increment differed by loading and increasing bytecode order.
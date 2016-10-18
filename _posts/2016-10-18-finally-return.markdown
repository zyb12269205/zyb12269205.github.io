---
published: true
title: Finally Return
layout: post
---
Finally Return
```java
public class SandBox {

   public static void main(String[] args){
       System.out.println(get("0"));
   }

    public static int get(String x){
        try{
            return Integer.parseInt(x);
        } finally {
            return -1;
        }
    }
}
```

It will always return -1.
return in try block will not be executed before finally has been executed.

The other example
```java
public class SandBox {

   public static void main(String[] args){
       System.out.println(get("0"));
   }

    public static int get(String x){
        try{
            return Integer.parseInt(x);
        } finally {
            //return -1;
        }
    }
}
```

It will print out 0.
return in finally will overwrite the return value stack (as it will always be executed).

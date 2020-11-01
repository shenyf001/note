# Java

## 单例

```java
public class Singleton {
    private Singleton() {}
    private static Singleton single=null;
    //静态工厂方法
    public static Singleton getInstance() {
         if (single == null) {  
             synchronized (Singleton.class) {  
               if (singleton == null) {  
                  singleton = new Singleton();
               }  
            }  

         }  
        return single;
    }
}
```

## JAVA线上问题处理，如何定位FullGC问题

[参考链接](https://blog.csdn.net/C18298182575/article/details/87484265)

## 如何设计对外提供的接口

## IOC和AOP

## cookie，session，token的区别


## http协议格式


## 浏览器登录过期机制









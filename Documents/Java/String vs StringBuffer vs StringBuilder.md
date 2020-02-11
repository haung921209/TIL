# `String` 의 특징

```java
String str = "abc";

//is equivalent to
char data[] = {'a', 'b', 'c'};
String str = new String(data);

//more examples
System.out.println("abc");
String cde = "cde";
System.out.println("abc" + cde);
String c = "abc".substring(2,3);
String d = cde.substring(1, 2);
```



`string`은 문자열을 저장하고 관리하는 기본적인 클래스입니다. 다른 두 클래스와 가장 큰 차이점은 바로 가변적이지 않다는 것입니다.(immutable) 이러한 특징에서, + 연산이나 `concat` 등을 이용해서 문자열에 변화를 주게 되면 본래의 메모리 공간은 변하지 않고 새로운 String 객체를 생성하는 것입니다. 이러한 방식의 단점은 기존 메모리 공간의 낭비(가비지 콜렉터에 의해 제거되기를 기다려야 함 **언제 제거될지 모름**)를 유발합니다.



```java
String test1 = "Hello ";
String test2 = "world";
System.out.println("결과");
System.out.println("test1 : " + test1);
System.out.println("test2 : " + test2);
System.out.println("test1의 주소공간 : " + test1.hashCode());
System.out.println("test2의 주소공간 : " + test2.hashCode());

test1 = test1 + test2;
System.out.println("test1 + test2의 주소공간 : " + test1.hashCode());

```

> 결과
>
> test1 : Hello 
> test2 : world
> test1의 주소공간 : -2137068114
> test2의 주소공간 : 113318802
> test1 + test2의 주소공간 : -832992604



대신, 불변하는 String의 특징은 고정된 값이 단순하게 읽히는 연산에서는 다른 클래스에 비해 빠르게 읽을 수 있는 장점이 있습니다.

## `StringBuffer` 의 특징

`StringBuffer`의 `String` Class와 구별되는 가장 큰 특징은 수정이 가능하다는 것입니다. 또한, `StringBuffer`의 가장 큰 특징은 thread-safe입니다. `StringBuffer`는 `StringBuilder`와 비교할 때 multiple thread에서 동기화를 보장합니다.



## `StringBuilder` 의 특징

`StringBuilder` Class 또한 `String` Class와 구별되는 특징은 수정이 가능하다는 것입니다. 하지만 `StringBuffer`와는 다르게, thread-safe를 보장하지 않습니다. 이는 multiple-thread 상황에서는 안정성을 위해 `StringBuffer`를 이용해야 한다는 것을 의미합니다. 반대로, single-thread가 보장되는 상황이라면 비교적 더 빠른 `StringBuilder`를 쓰는 것이 좋습니다. `StringBuilder`는 single-thread 상황이라면 `StringBuffer`와 비교하여 대부분의 경우에서 더 빠릅니다.



## `StringBuffer`와 `StringBuilder` Multi-thread test



```java
StringBuffer stringBuffer = new StringBuffer();
StringBuilder stringBuilder = new StringBuilder();

new Thread(() -> {
    for(int i=0; i<10000; i++) {
        stringBuffer.append(i);
        stringBuilder.append(i);
    }
}).start();

new Thread(() -> {
    for(int i=0; i<10000; i++) {
        stringBuffer.append(i);
        stringBuilder.append(i);
    }
}).start();

new Thread(() -> {
    try {
        Thread.sleep(50000);

        System.out.println("StringBuffer.length: "+ stringBuffer.length());
        System.out.println("StringBuilder.length: "+ stringBuilder.length());
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}).start();
```

> StringBuffer.length: 77780
> StringBuilder.length: 77623





## `StringBuffer`와 `StringBuilder` Single-thread test

```java
public static void main(String[] args) {
		stringBufferTest();
		stringBuilderTest();
	}
	public static void stringBufferTest() {
	      long startTime = System.nanoTime();
	      StringBuffer sb = new StringBuffer();
	      for (int i=0; i < 1000; i++) {
	         sb.append((char) 'a');
	      }
	      System.out.println("StringBuffer test time : " + (System.nanoTime() - startTime));
	   }
	   public static void stringBuilderTest() {
	      long startTime = System.nanoTime();
	      StringBuilder sb = new StringBuilder();
	      for (int i=0; i < 1000; i++) {
	         sb.append((char) 'a');
	      }
	      System.out.println("StringBuilder test time : " + (System.nanoTime() - startTime));
	   }
```

> StringBuffer test time : 71101
> StringBuilder test time : 27101







#### 출처

https://docs.oracle.com/javase/8/docs/api/java/lang/String.html

https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html

https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html

https://novemberde.github.io/2017/04/15/String_0.html

https://www.tutorialspoint.com/how-can-we-compare-a-stringbuilder-with-stringbuffer-in-java
# 3. Data Types in Java

<br>

## 1. PDT (Primitive Data Type) 

>  데이터 그 자체가 들어가 있는 타입

: 기본 데이터 형  => 딱 8개뿐! 

  -> 기억 공간에 데이터가 바로 있음

  -> `. (dot) 연산자`를 쓸 수 없음 => why? 주소가 아니라서!

   

### 1. 논리형  

- `boolean`   -  1bit

  : (true/false) -> JAVA는 0,1 허용하지 않음

<br>

### 2. 문자형

- `char `    - 2byte

  ex) ‘a’ -> 문자 하나만 가능

   => single quotation(‘’) 사용!! -> ASCII code 값으로 저장됨

<br>

### 3. 정수형  `byte`     -   8bit (1 byte)  -128 ~127

- `Short` 

  : 16 bit (2 byte)

-  `Int`          

  : 32bit (4 byte)  => 정수형의 기본은 Int

- `Long`  

  : 64bit (8 byte)

<br>

### 4. 실수형   

- `float`      

  : 32bit (4 byte)

- `Double`       

  : 64bit (8 byte)   => 실수형의 기본은 Double

<br>



-> 위의 8개 제외하고는 다 Reference Type!!!!!

<br><br>

## 2. Reference Type 

> 주소가 들어가 있는 타입

: 참조 데이터 형

- 기억 공간에 주소가 들어가고 주소를 찾아 들어가야지만 실질적인 데이터가 있음

- `. (dot) 연산자` 쓸 수 있음!!  ex) 주소.

- Reference형에서는 String 빼고는 다 new 써야함

- String은 기본형처럼 쓸 수도 있고, new 쓸 수도 있음!!
  - New는 Heap영역에 올라감

  - 기본형 처럼 쓰면 new가 아닌 다른 영역에 올라감 => 이게 데이터 소모가 적음!

    ex) String address = new String(“비트캠”);  -> new 썼을 때

    ​       String address = “비트캠”;   -> 기본형처럼 썼을 때

<br>

<br>

#### String은 immutable한 (불변의) 객체이다!

 -> 그래서 String 의 데이터를 바꾸려면 String Builder나 String Buffer를 써야 함

<br>

#### Buffer 

= temporary 한 기억공간 (임시 공간)

 <br>

 #### null 값 

= 참조형에서 주소가 없는것을 명시적으로 알려주는 값

   ex) now = null;

<br>

<br>

#### Java는 연산자를 기준으로 타입을 일치시키려고 함!!

 ex 1)

```
 1 / 2 => 0

 1 / 2. => 0.5
```

   -> 실수형으로 type을 일치 시킴 (1을 1.0으로)

​	=> 정수형에서 실수형으로 바꾸는 과정에서 데이터 손실이 없으므로 자동으로 `type promotion` 일어남

<br>

ex 2)

```
int a = 1 + 1;   = 2

String b = “1” + “1”;  = “11”         

String c = 1 +1 + 1 + “1”  = “31”
```

 -> 결과값이 문자열이므로 타입을 String으로 선언함

​	=> 결과 값이 무엇이냐에 따라 타입이 달라진다!

<br>

<br>

#### char type & int type

`char type`은  `int type`으로 자동 *promotion*이 발생함!

 => but, int를 char로 바꾸려면 *type casting*을 해야함   

-> why? 데이터 소모가 있기 때문!

​     : char 2 byte    <   int 4 byte



*큰 사이즈에서 작은 사이즈로 가려면 데이터 소모가 있으므로 type casting을 해라!*



<br>

(정리)

큰 사이즈 -> 작은 사이즈 => 데이터 소모 있음 ⇒ `Type Casting`

작은 사이즈 -> 큰 사이즈 => 데이터 소모 없음 ⇒ `Promotion`

<br><br>



(Type Promotion in JAVA)

![img](https://lh3.googleusercontent.com/KXOWKRk-kEyIoztoda2M7RfldyM5UmDQKPNULtwcq5_UduHG7bhd9DFu1aaVHlGdLSgs91bdaQiKdPpygaduHFRi5Ew2pF6_kIHPhOKqc4jXuRI0ZUsQ0vEI3fXAd05i7YOmpMEF)

<br><br>

## Variables

<br>

### 1. Member variable

```
Class A {

 String name; 

}                  
```

- Class의 일원

- class 안에서 선언된 변수

- 초기값을 설정하지 않으면 자동 default 초기화가 됨  

  ex) String name = null;  할 필요 없음!

<br>

### 2. Local variable

```
Public Static Void main(~~~) {  

	String name;

}
```

- 함수의 일원

-  method(함수) 안에서 선언된 변수

-  default 초기화가 안됨  

  ex) String name = null; 해줘야 함



<br><br>



#### Null Assign을 하는 이유 (from docs.oracle)

: **Assign null to Variables That Are No Longer Needed**

Explicitly assigning a null value to variables that are no longer needed helps the garbage collector to identify the parts of memory that can be safely reclaimed. Although Java provides memory management, it does not prevent memory leaks or using excessive amounts of memory.

An application may induce memory leaks by not releasing object references. Doing so prevents the Java garbage collector from reclaiming those objects, and results in increasing amounts of memory being used. Explicitly nullifying references to variables after their use allows the garbage collector to reclaim memory.

One way to detect memory leaks is to employ profiling tools and take memory snapshots after each transaction. A leak-free application in steady state will show a steady active heap memory after garbage collections.



<br>

*다 쓰고 난 자원은 null assign을 해야한다! *

-> null assign을 하지 않으면 자원을 많이 먹어서 성능이 안좋아지기 때문!

<br>

 But, null assign 한다고 모든 자원이 반납되는게 아니다

```
input.close();

Input = null;
```

  -> 이렇게 해야 다 반납 할 수 있음
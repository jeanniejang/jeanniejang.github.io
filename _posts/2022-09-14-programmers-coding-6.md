---
title: "Programmers Q6. 정수 제곱근 판별"
categories: Algorithm
tag: [Java, Programmers, Easy-Algorithm]
toc: true
---

📈 What I learned after solving the algorithm questions.
{: .notice}

## [문제 링크(Question link)](https://school.programmers.co.kr/learn/courses/30/lessons/12934)

## Approach:
x 곱하기 x 했을 때 n이 나오면 (x+1) 곱하기 (x+1)을 하고 아니면 -1을 리턴한다.

## Solution:
Java의 Math class의 제곱근 구하기와 거듭제곱 구하기를 사용하면 된다. 혹은 접근방식 그대로 코드를 짜도 된다.

### Code 1: using Math class
```java
class Solution6 {
  public long solution(long n) {
      if (Math.pow((int)Math.sqrt(n), 2) == n) {
            return (long) Math.pow(Math.sqrt(n) + 1, 2);
        }
        return -1;
  }
}

    public static void main(String[] args) {
        Solution6 solution6 = new Solution6();
        long answer = solution6.solution(121);
        System.out.println("answer = " + answer);
    }
}
```

### Code 2: using for loop
```java
class Solution6 {
    public long solution(long n) {
        long answer = 0;
        for (long x = 1; x < n; x++)
            if (n == x * x) {
                answer = (x + 1) * (x + 1);
                break;
            } else {
                answer= -1;
            }
        return answer;
    }

    public static void main(String[] args) {
        Solution6 solution6 = new Solution6();
        long answer = solution6.solution(121);
        System.out.println("answer = " + answer);
    }
}
```


## What I learned:
Math class를 사용하려고 했는데 테스트가 일부만 통과되고 실패하는 것들이 몇 개 있었다. 아래가 내가 원래 짠 코드다.

### Code I first wrote(few tests failed)
```java
public class Solution6 {
    public long solution(long n) {
        if (Math.pow(Math.sqrt((double) n), 2) == n) {
            double x = (Math.sqrt((double) n));
            return (long) Math.pow(x + 1, 2);
        } else {
            return -1;
        }
    }
}
```
분명히 제대로 썼는데 왜 안되냐고??하면서 의문에 가득 찼음. 다른 코드들이랑 비교해보니 type을 바꿔주는 위치에 문제가 있었다. 이미 주어진 n을 ```long```에서 ```double```로 바꿀 게 아니고 구해진 제곱근의 수가 long인지, 즉 정수인지 확인하는 게 중요했다. 아마 소수점이 있는 double의 제곱근을 다시 거듭제곱해도 n이 나오는 경우의 수가 있는 모양이다. 이 김에 data type을 다시 정리해봤다.

### Data Types
There are two data types used in Java;
 - Primitive data types
 	- Numbers
 	- Booleans
 	- Character
 - Non-primitive data types
 	- String
 	- Array
 	- etc.

Primitive data types are predefined and cannot be null.

#### Number types
Boolean and Characters are the data types itself but numbers can be divided once more into two different groups:

- Integer types
	- byte
	- short
	- int
	- long
- Floating point types
	- float
	- double

**Integer** is a whole number that can be positive, negative or 0, so obviously **integer types** only have a whole number as a value.

For the numbers with decimals, **floating point types** are used.

The **most used ones** are ```int``` and ```double``` respectively from each numeric types.
Also, when using ```long```, the value should always end with **L**.
```
ex)long n = 10000000000L;
```

Below is the diagram of the data types from [GeeksforGeeks](https://www.geeksforgeeks.org/data-types-in-java/).

![](https://i.imgur.com/S4L60bs.png)

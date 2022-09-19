---
title: "Programmers Q5. 평균 구하기"
categories: Algorithm
tag: [Java, Programmers, Easy-Algorithm]
toc: true
---

📈 What I learned after solving the algorithm questions.
{: .notice}

## [문제 링크(Question link)](https://school.programmers.co.kr/learn/courses/30/lessons/12944)

## Approach:
모든 수를 더한 후에, 그 수의 개수로 나누면 평균값을 구할 수 있다. 

## Solution:
for loop을 돌려서 각 인덱스의 수를 더해 int 배열의 총합을 구한다. 배열의 길이가 배열 안에 있는 수의 총 개수이므로 구한 총합을 배열의 길이의 수로 나누어준다.

### Code 1: using if statement
```java
public class Solution5 {
    public double solution(int[] arr) {
        double answer = 0;
        for(int i = 0; i<arr.length; i++){
            answer+=arr[i];
        }
        return answer/arr.length;
    }

    public static void main(String[] args) {
        Solution5 solution5 = new Solution5();
        int[] arr = {1,2,3,4};
        double answer = solution5.solution(arr);
        System.out.println("answer = " + answer);
    }
}
```

## What I learned:
문제풀이에 사용한 ```length```와 ```length()```의 차이에 대해서 정리해보았다. 늘 그냥 이거 아닌가?저건가? 하면서 해보고 오류 나면 바꾸는 식으로(...) 마구잡이로 썼는데 이번 기회에 정리한다.

### Difference between ```length``` and ```length()```

```array.length``` is **applicable for an array** to know the length of it. It can be used for any arrays such as int[], char[], double[], String[].
For example, if there is a String array;
```java
String[] str={apple, banana, orange}
int n = str.length;  // counts how many words there are in the array
n = 3
```

On the other hand, ```string.length()``` is **applicable for string objects**, such as String, StringBBuilder, etc. This method returns the number of characters in the string.
For example, if there is a String;
```java
String str = "Hello";
int n = str.length();
n = 5
```
```length()``` can't be used in array, so if I want to know the length of a word in a String array, I would have to pick the word out first from the array as follows;
```java
String[] str={apple, banana, orange}
int n = str[0].length(); //picking the 0th word from the array
n = 5   //length of the word "apple" in the array
```
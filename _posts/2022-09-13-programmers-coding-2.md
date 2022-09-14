---
title: "Programmers Q2. 짝수와 홀수"
categories: Algorithm
tag: [Java, Programmers, Easy-Algorithm]
toc: true
---

📈 What I learned after solving the algorithm questions.
{: .notice}

## [문제 링크(Question link)](https://school.programmers.co.kr/learn/courses/30/lessons/12937)
> 출처: 프로그래머스 코딩 테스트 연습, https://school.programmers.co.kr/learn/challenges

## Approach:
짝수면 2로 나눴을 때 나머지 0, 홀수면 나머지 1.

## Solution:
modulus 사용해서 num의 나머지 값을 구한다. 만약 0이면 Even, 그 외에는 Odd를 리턴한다.

### Code 1: using if statement
```java
public class Solution2 {
    public String solution(int num) {
        String answer;
        if (num % 2 == 0){
            answer = "Even";
        }else {
            answer = "Odd";
        }
        return answer;
    }


    public static void main(String[] args) {
        Solution2 solution2 = new Solution2();
        String answer = solution2.solution(4);
        System.out.println("answer = " + answer);
    }
}
```

## What I learned:
간단한 if문을 줄이기 위해 ternary operator을 사용할 수 있다. 사용을 해보려고 했는데 수식을 정확하게 알지 못해서 사용하지 못했다. ```if(num%2==0) ? "Even" :"Odd";``` 이런 식으로 쓰니까 안됐는데 다시 찾아보니 ```if()``` 자체를 뺐어야 했다. 다음엔 꼭 제대로 쓰자.

### Code refactored: using Tenery operator
```java
public class Solution2 {

    public String solution(int num) {
        return num % 2 == 0 ? "Even" : "Odd";
    }


    public static void main(String[] args) {
        Solution2 solution2 = new Solution2();
        String answer = solution2.solution(4);
        System.out.println("answer = " + answer);
    }
}
```


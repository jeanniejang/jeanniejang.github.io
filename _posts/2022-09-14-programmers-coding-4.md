---
title: "Programmers Q4. 약수의 합"
categories: Algorithm
tag: [Java, Programmers, Easy-Algorithm]
toc: true
---

📈 What I learned after solving the algorithm questions.
{: .notice}

## [문제 링크(Question link)](https://school.programmers.co.kr/learn/courses/30/lessons/12928)

## Approach:
약수(divisor)란 숫자를 나누었을 때 나누어 떨어지게 하는 수이므로 나머지가 0인 수를 모두 구해서 더하면 된다.

## Solution:
modulus 사용해서 n의 나머지 값을 구한다. 만약 나머지가 0이면 answer에 더해준다. 이 때, 나누는 수 x는 n보다 작거나 같다.


### Code 1: using if statement
```java
public class Solution4 {
    public int solution(int n) {
        int answer = 0;
        int x;
        for(x=1;x<=n;x++){
            if(n % x == 0){
                answer+=x;
            }
        }
        return answer;
    }

    public static void main(String[] args) {
        Solution4 solution4 = new Solution4();
        int answer = solution4.solution(12);
        System.out.println("answer = " + answer);
    }
}
```

## What I learned:
매우 간단하게 풀어서 좋아했는데 다른 사람의 풀이를 보고 놀랐다.
주어진 수를 2로 나누면 그를 초과하는 수에서는 자기 자신 말고는 더이상 약수가 없다. 그러므로 for loop을 돌릴 때 ```n```만큼 돌리지 말고 ```n/2```만큼만 돌려주면 주어진 수를 제외한 모든 약수를 구할 수 있다. 이 모든 약수들을 더해주고 마지막에 주어진 수를 더해주면 합을 구할 수 있다. 반복문을 반으로 줄일 수 있는 방법이다.

### Code refactored: less looping
```java
public class Solution4 {
    public int solution(int n) {
        int answer = 0;
        int x;
        for(x=1;x<=n/2;x++){
            if(n % x == 0){
                answer+=x;
            }
        }
        return answer+n;
    }

    public static void main(String[] args) {
        Solution4 solution4 = new Solution4();
        int answer = solution4.solution(12);
        System.out.println("answer = " + answer);
    }
}
```
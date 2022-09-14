---
title: "Programmers Q1: 나머지가 1이 되는 수 찾기"
categories: Algorithm
tag: [Java, Programmers, Easy-Algorithm]
toc: true
---

📈 What I learned after solving the algorithm questions.
{: .notice}

## [문제 링크(Question link)](https://school.programmers.co.kr/learn/courses/30/lessons/87389)

## Approach:
처음 푼 문제인데 n-1을 해서 나뉘어 떨어지는 가장 작은 수를 리턴하면 되겠다는 생각을 했다. 하지만...식으로 어떻게 접근해야할지 감이 잡히지 않았다. 30분 고민한 결과, 다른 사람들의 풀이를 봤다.

## Solution:
결과적으로 접근은 틀리지 않았다. (사실 쉬운 문제라 접근이 틀리기는 쉽지 않음...)
문제 조건에서 n의 최소값이 3이므로 x의 최소값은 2이다. 그리고 x는 무조건 n보다는 작은 수이다.(x가 가장 클 수 있는 건 n-1)
그래서 for문을 돌리고 n 나누기 x의 값이 1이 나오면 x를 리턴하고 거기서 반복문을 종료한다.

### Code:
```java
class Solution1 {
    public int solution(int n) {
        int answer = 0;
        for (int x = 2; x < n; x++) {
            if (n % x == 1) {
                answer = x;
                break;
            }
        }
        return answer;
    }

    public static void main(String[] args) {
        Solution1 solution1 = new Solution1();
        int x = solution1.solution(11);
        System.out.println("x = " + x);
    }
}
```

## What I learned:
나머지를 구하기 위한 operator은 %(modulus)를 쓴다.
반복문을 돌릴 때, 가장 처음에 필요한 값이 나왔을 때 멈추길 바라면 break를 걸어준다.
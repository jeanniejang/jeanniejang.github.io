---
title: "Programmers Q3. 자릿수 더하기"
categories: Algorithm
tag: [Java, Programmers, Easy-Algorithm]
toc: true
---

📈 What I learned after solving the algorithm questions.
{: .notice}

## [문제 링크(Question link)](https://school.programmers.co.kr/learn/courses/30/lessons/12931)

## Approach:
처음에는 int n을 char로 만들어서 각 index의 값을 가져와 더하려고 했다. 하지만 정해진 시간 안에 하려다보니 안될 것 같아서 다른 방법으로 선회했다. int n을 10으로 나눠서 그 나머지를 구하고, 나눈 값을 또 10으로 나누고 해서 나머지 값을 모두 더하면 된다.


## Solution:
modulus 사용해서 n의 나머지 값을 구한다. 10의 단위로 나누기 때문에 나머지에 1의 자리 숫자가 나온다. 그 나머지값을 저장한다. 그 다음에 n을 10으로 나눈 값으로 다시 저장을 해준다. 새로운 n을 다시 10으로 나눈다. n이 0이 될 때까지 반복한다.

### Code:
```java
public class Solution3 {
    public int solution(int n) {
        int answer = 0;
        while(n!=0) {
            answer = n % 10 + answer;
            n = n/10;
        }
        return answer;
    }

    public static void main(String[] args) {
        Solution3 solution3 = new Solution3();
        int n = 987;
        int answer = solution3.solution(n);
        System.out.println("answer = " + answer);
    }
}
```


## What I learned:
코딩테스트 문제를 풀 때는 정말 어떻게 생각하는지가 중요한 것 같다. String으로 바꿔서 그 인덱스를 구해서 하는 것보다 간단한 연산으로 풀 수 있는 문제였는데 어렵게 생각했다.중요한 건 효율성이다.
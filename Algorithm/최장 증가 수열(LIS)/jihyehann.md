# 💡 최장 증가 수열 (LIS)

## LIS (Longest Increasing Subsequence) 란?

최장 증가 (부분) 수열

원소가 n개인 배열의 일부 원소를 골라내서 만든 부분 수열 중, 각 원소가 이전 원소보다 크다는 조건을 만족하고, 그 길이가 최대인 부분 수열.

예시

- { 6, **2**, **5**, 1, **7**, 4, **8**, 3} &rarr; { 2, 5, 7, 8 }
- { 7, **2**, **3**, 8, **4**, **5** } &rarr; { 2, 3, 4, 5 }

<br/>

## 구현 방법

구현 방법에는 2가지가 있다.

1. DP를 이용하는 방법 : $O(N^2)$
2. 이분탐색을 이용하는 방법 : $O(NlogN)$

<br/>

### 1. DP :  $O(N^2)$

예시 문제 : [백준 11053번](https://www.acmicpc.net/problem/11053)

- N (1 ≤ N ≤ 1,000)
- 가장 긴 증가하는 부분 수열의 길이 구하기


```c
#include <algorithm>
using namespace std;

int n, arr[1001];
int lis() {
    int dp[1001] = {0};
    for(int i=1; i<n; i++) {
        for(int j=i-1; j>=0; j--) {
            if(arr[i] > arr[j]) 
            	dp[i] = max(dp[i], dp[j]+1);
        }
    }

    int answer = 0;
    for(int i=0; i<n; i++)
        answer = max(answer, dp[i]);
    
    return answer+1;
}
```

<br/>

### 2. lower bound (이분 탐색) : $O(NlogN)$

예시 문제 : [백준 12015번](https://www.acmicpc.net/problem/12015)

- N (1 ≤ N ≤ 1,000,000)
- 가장 긴 증가하는 부분 수열의 길이 구하기

해결 방법

- 이분 탐색을 이용한다.
- 부분 수열의 마지막 숫자를 저장할 리스트를 만든다.
- 배열의 원소가 리스트의 맨마지막 원소보다 크면, 리스트에 추가한다. <br/>
같거나 작으면, lower bound 위치를 해당 값으로 대체한다. 
- `lower bound` : 주어진 값보다 크거나 같으면서 제일 작은 값
- 이렇게 하여 만들어진 리스트의 원소 개수가 최종적으로 최장 증가 수열의 개수가 된다.

ex)

0 8 4 12 2 10 6 14 1 9

1. 0
2. 0 **8** (8 추가)
3. 0 **4** (4로 대체)
4. 0 4 **12** (12 추가)
5. 0 **2** 12 (2로 대체)
6. 0 2 **10**  (10으로 대체)
7. 0 2 **6** (6으로 대체)
8. 0 2 6 **14** (14 추가)
9. 0 **1** 6 14 (1로 대체)
10. 0 1 6 **9** (9로 대체)

&rarr; 최장 증가 수열의 길이 : 4

```c
#include <algorithm>
#include <vector>
using namespace std;

int n, arr[1000001];
int lis() {
    vector<int> list;
    list.emplace_back(arr[0]);
    for(int i=1; i<n; i++) {
        if(arr[i] > list.back()) // 맨마지막 원소보다 큰 경우
            list.emplace_back(arr[i]);
        else { // 같거나 작은 경우
            auto it = lower_bound(list.begin(), list.end(), arr[i]);
            *it = arr[i];
        }
    }
    return list.size();
}
```

<br/>

## 🔖 참고

- [gyoogle](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/LIS%20(Longest%20Increasing%20Sequence).md)
- [블로그](https://eine.tistory.com/entry/%EA%B0%80%EC%9E%A5-%EA%B8%B4-%EC%A6%9D%EA%B0%80%ED%95%98%EB%8A%94-%EB%B6%80%EB%B6%84-%EC%88%98%EC%97%B4LIS-Longest-Increasing-Subsequence)

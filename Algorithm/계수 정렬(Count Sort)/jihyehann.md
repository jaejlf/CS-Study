# 💡 계수 정렬(counting sort)

비교 연산을 하지 않고 정렬하는 알고리즘.

정렬하는 숫자가 특정한 범위 내에 있을 때 사용한다.

<br/>

## 1. 알고리즘
1. 입력 배열의 최댓값, counting 배열 생성  
    - 원소의 누적합을 구하기 위한 counting 배열  생성을 위해 입력 배열의 최댓값이 필요하다. 
    - 최댓값 + 1 크기의 Counting Array를 생성한다.

2. 원소 개수를 count하여 counting 배열에 저장
    - 입력 배열의 값을 기준으로 조회된 좌표에 입력 배열의 각 원소 개수를 count 한다.

3. counting 배열을 누적합 배열로 만들기
    - 이전 좌표의 원소 개수를 더해나가 `누적합` 배열로 만들어준다.

4. 입력 배열과 누적합 배열을 이용한 정렬 수행
    - 입력 배열의 각 원소를 counting 배열에서 조회하여 어느 좌표에 들어가야 하는지 체크한 뒤 조회된 원소의 개수를 1 감소시켜 앞의 좌표로 입력받을 수 있게 한다.

![counting sort](https://user-images.githubusercontent.com/75151848/193446619-42ee17b3-11c9-43cc-8269-0de86b686822.gif)


<br/>

## 2. 구현
### Java
```java
public static void countSort(int[] arr) {
  int max = Arrays.stream(arr).max().getAsInt();
  int min = Arrays.stream(arr).min().getAsInt();
  int range = max - min + 1;
  int count[] = new int[range];
  int output[] = new int[arr.length];
  
  // 모든 요소에 대해서 count
  for (int i = 0; i < arr.length; i++) {
    count[arr[i] - min]++;
  }

  // 누적합 계산
  for (int i = 1; i < count.length; i++) {
    count[i] += count[i - 1];
  }

  // 뒤에서부터 배열을 돌면서, 해당하는 값의 인덱스에 값 넣어주기
  for (int i = arr.length - 1; i >= 0; i--) {
    output[count[arr[i] - min] - 1] = arr[i];
    count[arr[i] - min]--;
  }

  for (int i = 0; i < arr.length; i++) {
    arr[i] = output[i];
  }
}
```
<br/>

## 3. 시간복잡도

$O(n+k)$의 시간복잡도를 가진다.
- k : 정렬할 수들 중 가장 큰 값

> ❗️ k가 n보다 작은 수이면 O(n)이 되지만, k가 n보다 매우 큰 수이면 O(무한)이 될 수 있다.

<br/>

## 4. 공간복잡도

Auxiliary Space: $O(k)$

<br/>

## 5. 장점

- O(n) 의 시간복잡도를 가진다.

<br/>

## 6. 단점

- 배열 사이즈 N 만큼 돌 때, 증가시켜주는 Counting 배열의 크기가 커 메모리 낭비가 심하다.
- 가장 큰 숫자에 영향을 받는다.


<br/>

## 🔖 참고
- [Counting Sort](https://www.geeksforgeeks.org/counting-sort/?ref=lbp)
- [계수 정렬(Counting Sort)](https://gyoogle.dev/blog/algorithm/Counting%20Sort.html)
- [카운팅 정렬(Counting Sort, 계수 정렬) 알고리즘](https://8iggy.tistory.com/123)

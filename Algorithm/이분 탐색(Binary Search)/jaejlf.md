# 📍 이분 탐색(Binary Search)

이진 탐색은 정렬된 리스트에서 검색 범위를 줄여 나가면서 검색 값을 찾는 알고리즘

<br>

## 동작 원리

1. 배열의 중간 값을 가져온다.
2. 중간 값과 검색 값을 비교한다.

    a. 중간 값이 검색 값과 같다면 종료한다. (mid = key)
    
    b. 중간 값보다 검색 값이 크다면 중간값 기준 배열의 오른쪽 구간을 대상으로 탐색한다. (mid < key)
    
    c. 중간 값보다 검색 값이 작다면 중간값 기준 배열의 왼쪽 구간을 대상으로 탐색한다. (mid > key)
    
3. 값을 찾거나 간격이 비어있을 때까지 반복한다.

<br>

## 검색

### 1. 먼저 배열의 가운데를 결정

![image](https://user-images.githubusercontent.com/78673570/197377381-290b04ba-0871-486b-a19d-65f4c4b65078.png)

<br>

### 2. 중앙 값과 검색 값을 비교

![image](https://user-images.githubusercontent.com/78673570/197377442-b2539bba-fb8e-46ab-8aa3-da6e446ebe15.png)

<br>

### 3. 중앙 값을 결정

![image](https://user-images.githubusercontent.com/78673570/197377458-9846a7a4-d451-4601-b4cf-2c79336913c1.png)

<br>

### 4. 중앙 값과 검색 값을 비교

![image](https://user-images.githubusercontent.com/78673570/197377471-27797b65-02b6-4ebf-ae75-4786c90e8acc.png)

<br>

### 5. 중앙 값을 결정

![image](https://user-images.githubusercontent.com/78673570/197377503-426dba4d-93b5-4387-94f9-6e290d662fd1.png)

<br>

### 6. 중앙 값과 검색 값을 비교

<br>

## 종료

### 1.검색을 성공할 경우

![image](https://user-images.githubusercontent.com/78673570/197377893-2d7d8745-1edc-4e79-bfc1-37405d568ed2.png)

<br>

### 2. 검색을 실패할 경우

![image](https://user-images.githubusercontent.com/78673570/197377917-439702b8-b5d6-4d28-a667-f743615a915a.png)

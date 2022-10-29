# 💡 다익스트라(Dijkstra) 알고리즘

## 다익스트라 알고리즘이란?

**가중치가 양수**인 무방향 그래프에서 시작점으로부터 각 정점으로 가는 **최단 경로**를 구하는 알고리즘.

![](https://velog.velcdn.com/images/wisdom-one/post/e882e9fa-436c-479f-b084-2cd8047eb544/image.png)

<br/>

## 동작 과정

1. 최단 거리 값은 무한대 값으로 초기화한다.
2. 시작 정점의 최단 거리는 0으로 설정한다.
3. 시작 정점과 연결된 정점들의 최단 거리 값을 갱신한다.
4. 최단경로를 체크하지 않은 정점 중 최단 거리가 최소인 정점을 찾는다.
5. 찾은 정점과 연결된 정점의 최단 거리 값을 갱신한다.
4. 모든 정점을 체크할 때까지 4~5 단계를 반복한다.

<br/>

## 구현 코드
```c
#include<vector>
#include<queue>
using namespace std;

#defind MAX_SIZE 1e6
#define INF 1e9 // 무한을 의미하는 값으로 10억을 설정

// 노드의 개수(N), 시작 노드 번호(Start)
int n, start;

// 각 노드에 연결되어 있는 노드에 대한 정보를 담는 배열
// 연결된 노드, 비용
vector<pair<int, int>> graph[MAX_SIZE]; 

// 최단 거리 테이블
int d[MAX_SIZE]; 

void dijkstra(int start, int n) {

    for (int i=1; i<=n; i++)
        d[i] = INF;
        
    priority_queue<pair<int,int>>pq; // 거리, 노드 인덱스 
    
    pq.push({0,start}); //시작 노드로 가기위한 최단 경로는 0으로 설정하여, 큐에 삽입.
    d[start]=0;
    
    while(!pq.empty()) {
        int dist = -pq.top().first; //현재 노드까지의 비용 (거리)
        int now = pq.top().second; // 현재 노드
        pq.pop();
        
        if(d[now] < dist) // 이미 최단경로를 체크한 노드인 경우 패스
            continue;
        
        for(int i=0; i<graph[now].size(); i++) {
            int cost = dist + graph[now][i].second; // 거쳐서 가는 노드의 비용을 계산
                                                    // 현재노드까지 비용 + 다음 노드 비용
            if(cost<d[graph[now][i].first]) { // 비용이 더 작다면 최단경로 테이블 값을 갱신
                d[graph[now][i].first]=cost;
                pq.push(make_pair(-cost,graph[now][i].first));
            }
        }
    }
}
```

<br/>

## 시간 복잡도

- 기본 알고리즘 시간복잡도 : $O(V^2)$ 
- 우선순위 큐를 이용 시 시간복잡도 : $O(ElogE)$


최단 거리가 최소인 정점을 찾을 때, 선형 탐색이 아닌 우선순위 큐를 사용하면 시간을 줄일 수 있다.

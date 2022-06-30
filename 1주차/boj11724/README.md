# 문제
```
방향 없는 그래프가 주어졌을 때, 연결 요소 (Connected Component)의 개수를 구하는 프로그램을 작성하시오.
```
### 입력
첫째 줄에 정점의 개수 N과 간선의 개수 M이 주어진다. (1 ≤ N ≤ 1,000, 0 ≤ M ≤ N×(N-1)/2) 둘째 줄부터 M개의 줄에 간선의 양 끝점 u와 v가 주어진다. (1 ≤ u, v ≤ N, u ≠ v) 같은 간선은 한 번만 주어진다.
### 출력
첫째 줄에 연결 요소의 개수를 출력한다.
### 테스트 케이스
| 입력 | 결과 |
|:---:|:---:|
| 6 5 <br> 1 2 <br> 2 5 <br> 5 1<br> 3 4 <br> 4 6 <br> | 2 |
| 6 8 <br> 1 2 <br> 2 5 <br> 5 1 <br> 3 4 <br> 4 6 <br>5 4 <br>2 4<br> 2 3 <br> | 1 |

### 제출 코드


```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(100000) ## 재귀횟수 에러가 나서
n, m = map(int,input().rstrip().rsplit())
graph, visited = {}, [0]*(n+1)
cnt = 0

for _ in range(m):
    u,v = map(int,input().rstrip().rsplit())
    if u not in graph:
        graph[u] = [v]
    else:
        graph[u].append(v)

    if v not in graph:
        graph[v] = [u]
    else:
        graph[v].append(u)

def dfs(u):
    visited[u] = 1
    if u in graph:
        for v in graph[u]:
            if visited[v] == 0:
                dfs(v)

    return 1

for i in range(1,n+1):
    if visited[i] == 0:
        cnt += dfs(i)

print(cnt)
```


### 디버깅 편한 코드


```python
from collections import defaultdict

def solution(inputArr):
    global graph, visited
    n,m = inputArr[0]
    arr = inputArr[1:]
    answer = 0
    graph = defaultdict(list)
    visited = defaultdict(bool)
    for i in range(m):
        u,v = arr[i]
        graph[u].append(v)
        graph[v].append(u)
        visited[u] = 0
        visited[v] = 0
    for i in range(1,n+1):
        if not visited[i]:
            answer += dfs(i)
    return answer

def dfs(u):
    visited[u] = 1
    if u in graph:
        for v in graph[u]:
            if visited[v] == 0:
                dfs(v)
    return 1
```

### 테스트 케이스 1


```python
solution(
    [
        [6,5],
        [1,2],
        [2,5],
        [5,1],
        [3,4],
        [4,6]
    ]
)
```




    2



### 테스트 케이스 2


```python
solution(
    [
        [6,8],
        [1,2],
        [2,5],
        [5,1],
        [3,4],
        [4,6],
        [5,4],
        [2,4],
        [2,3]
    ]
)
```




    1



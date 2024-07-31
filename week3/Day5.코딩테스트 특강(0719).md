# 코딩 테스트 팁
# 목적

- 공개채용 필터링
- 수시채용에서 잘 하는 사람을 뽑기 위해
- 알고리즘 대회

# 준비 방법

## 기초 구현 능력

알고리즘 평가가 아닌 프로그래밍 순수 실력을 보는 평가가 등장

즉 알고리즘의 이해보다는 요구사항 분석, 구현 능력 자체가 중요해지고 있음

기초적인 구현 문제를 꾸준히 풀어야 성장하는 능력

## 기초 알고리즘 능력

고급 알고리즘 문제의 출제 빈도가 줄어들고 기초 알고리즘 문제의 빈도가 많아짐 

기초 알고리즘을 응용하는 정도의 난이도이며 특정 산업 분야에서는 복잡한 요구 사항을 최적화할 수 있는 알고리즘을 구현하는 것을 목표로 하는 문제도 등장

## 요구 사항 파악하기

문제를 틀리는 원인 중 요구 사항을 놓치는 경우가 많음

“이럴 것이다”라는 추측은 문제에 반영하면 안 됨

문제를 잘 해결하려면 제출한 코드에 대한 문제의 요구 사항을 정리해야함

요구 사항 파악 능력을 키우는 방법은 문제에 대해 내가 해결해야하는 부분과 구현하는 부분을 분리하여 문제에 대한 요구 사항만 분석해보는 것

## 공부 방법

왕도는 없음

개별적인 티칭이 가장 빠른 방법이긴 하나 여건이 모두 안되기 때문에 스터디를 하는 것이 좋음

“잘 하는 사람” 중심으로 모이는 경우가 잘 되는 스터디. 개념을 잘 이해한 사람이 스터디를 이끌기 때문에 주변 친구들 중 잘 찾아보는 것이 좋음

스터디 구성하고 문제를 무작정 많이 푸는 것은 의외로 지치고 도움이 안될 수 있으니 문제 풀이와 코드를 분석해보는 과정이 중요

## 응시 경험, 모의고사

모의 시험이나 실제 코딩 테스트 환경을 경험해보는 것이 좋음

하나도 풀지 않고 나와도 되지만 문제 복기를 반드시 하고 나중에 풀어보면 좋음

프로그래밍 문제를 만드는 사람은 점점 줄어드는 추세이고 기업 별로 문제 은행을 모으는데 집중하고 있음

## 자신감

떨어져도 된다는 마음, 일단 본다는 마음으로 ㅇ응시

코테를 두려워하고 피하기 시작하는 순간 지원 가능한 회사는 반으로 줄어듦

사실상 공기업/금융권은 모두 포기하고 포트폴리오만 보는 회사를 준비해야 함

# Q&A

## 기본적으로 학습해야 하는 알고리즘 주제

정렬, 그래프 탐색(dfs/bfs), dp, 우선순위 큐, 문자열 알고리즘, 완전 탐색(투포인터)

## 풀지 못한 문제를 다시 풀 수 있을 떄까지 학습하는 방법

2시간을 고민해보고 근처에도 못가면 그 알고리즘을 모르는 것, 이런 경우 해설지를 보며 학습

만약 풀었는데 실수한거면 체크해놓고 다시 실수하지 않도록 해야함

## 히든케이스를 잡는 팁

소수를 많이 찾는 것이 좋음

격자형 문제에서 n*n의 문제가 있다면 7*7, 11*11 등의 엣지 케이스를 만들어보는 것이 좋음

# 모의 코테 복기
# 1번. 나무꾼 구름이 (100/100)

```python
import sys

input = sys.stdin.readline

n, m, k = map(int,input().split())
tree = list(map(int,input().split()))
r = int(input())
arr = list(input().split())
point = k - 1
answer = 0
d = dict()
grow = 0

for i in range(r):
	length = tree[point] + i
	if length >= m:
		if point not in d:
			d[point] = i
			answer += length
			tree[point] = 0
		else:
			if length - d[point] >= m:
				answer += length - d[point]
				d[point] = i
				tree[point] = 0
				
	if arr[i] =="R":
		point = (point + 1) % n
	elif arr[i] == "L":
		point -= 1
		if point == -1:
			point = n - 1
			
print(answer)
```

- python의 dictionary의 접근 속도는 O(1)이라는 것을 이용
- 나무를 자르면 자를 때의 길이를 기억해서 dictionary에 저장
- 시간 복잡도 : O(n)으로 상정

# 2번. 판다는 귀여워 (40/100) 제한시간 5초

```python
import sys

input = sys.stdin.readline

n,m,k = map(int,input().split())
arr = [[0 for _ in range(m)] for _ in range(n)]

for i in range(k):
	p_x, p_y = map(int,input().split())
	for x in range(n):
		for y in range(m):
			arr[x][y] += abs((x + 1) - p_x)**2 + abs((y + 1) - p_y)**2

answer = 10**9
for x in range(n):
	for y in range(m):
		answer = min(answer, arr[x][y])
	
print(answer)
```

- 판다가 위치한 곳의 예외처리를 하지 못했음
- n, m, k의 최대 값이 100이므로 3중 for문을 사용해도 1,000,000
- 파이썬의 시간복잡도는 대략 1초당 2000만번 연산이므로 넉넉

### 예외처리한 코드

```python
import sys

input = sys.stdin.readline

n, m, k = map(int, input().split())
arr = [[0 for _ in range(m)] for _ in range(n)]

for i in range(k):
    p_x, p_y = map(int, input().split())
    arr[p_x][p_y] = -1
    for x in range(n):
        for y in range(m):
            if p_x == x and p_y == y:
                continue
            arr[x][y] += abs((x + 1) - p_x) ** 2 + abs((y + 1) - p_y) ** 2

answer = 10 ** 9
for x in range(n):
    for y in range(m):
        if arr[x][y] == -1:
            continue
        answer = min(answer, arr[x][y])

print(answer)
```

# 3번. 택시 기사 구름이 (100/100) 제한시간 8초

```python
from collections import deque

def copy_map():
	co_arr = [[-arr[i][j] for j in range(n)] for i in range(n)]
	return co_arr

def bfs(x, y, target_x, target_y):
	num = 2
	q = deque([(x, y, num)])
	co_arr[x][y] = 1
	while q:
		x, y, num = q.popleft()
		for dx, dy in move:
			nx, ny = x + dx, y + dy
			if nx >= n or ny >= n or nx < 0 or ny < 0: continue
			if co_arr[nx][ny] != 0 : continue
			q.append([nx, ny, num + 1])
			co_arr[nx][ny] = num
			if nx == target_x and ny == target_y:return

	
n, m = map(int,input().split())
basic, extra, fee = map(int, input().split())
arr = [list(map(int,input().split())) for i in range(n)]
move = [(1,0), (-1,0), (0,1), (0,-1)]
answer = 0
start_x, start_y = -1, -1
co_arr = []

for i in range(m):
	a, b, c, d = map(int,input().split())
	a,b,c,d = a-1, b-1, c-1, d-1
	if start_x + start_y != -2:
		co_arr = copy_map()
		bfs(start_x, start_y, b, a)
		answer -= (co_arr[b][a] - 1) * fee
		
	co_arr = copy_map()
	bfs(b, a, d, c)
	dist = co_arr[d][c] - 1
	if dist <= 5:
		answer += basic
	else:
		answer += basic + (dist - 5) * extra
	answer -= dist * fee
	start_x, start_y = d, c
	
print(answer)
```

- bfs에서 각 지점의 최단 거리를 저장
- 맵을 카피하며 가지 못하는 부분은 -1 처리
- 타겟 지점에 도착하면 return하여 최적화

---
layout: post
title: "분리 집합 (Disjoint set) : Union - Find"
excerpt_image: /assets/images/union.png
categories: Algorithm
tags: [Algorithm]
---

# 분리 집합 (Disjoint set) : Union - Find

분리 집합은 서로소 집합이다. 분리 집합을 가장 빠르고 쉽게 알아보는 알고리즘으로 **Union-Find** 가 있다. 여러 개의 노드가 존재할 때 두 개의 노드를 선택해서, **두 개의 노드가 같은 집합에 속하는지 판별**하는 알고리즘이다.

Union-Find 는 일차원 배열 한개로 간단하게 구현할 수 있으니, 구현은 마지막에 알아보고 알고리즘의 원리부터 알아보겠다. 위 알고리즘은 두개의 연산을 전제로 한다.

- Find(X) : X가 속한 집합의 대표값(루트 노드)을 반환한다
- Union(X, Y) : X가 속한 집합과 Y가 속한 집합을 합친다

먼저, 모든 노드가 자기 자신을 가르키도록 배열을 초기화한다. 현재 상태는 집합의 원소를 5개 만들었다고 볼 수 있다.

![Untitled](/assets/images/union.png)

| node | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| value | 1 | 2 | 3 | 4 | 5 |

예를 들어, 모든 원소를 하나의 집합으로 합치는 경우를 보겠다. Union-Find 는 트리 형태로 구현되기 때문에 아래와 같이 그림을 나타냈고 실제로는 하나의 집합이다. 대표값을 1로 가지고 원소가 5개인 하나의 집합이 완성되었고, Find(5) 연산을 했을 때 대표값인 1이 반환된다.

![Untitled](/assets/images/union-1.png)

| node | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| value | 1 | 1 | 2 | 3 | 4 |

다음으로 대표값을 1로 가지고 원소가 3개인 집합 X, 대표값을 4로 가지고 원소가 2개인 집합 Y를 살펴보겠다. 아래와 같은 상황에서 Find(3) 연산을 하면 대표값인 1이 Find(5) 연산을 하면 대표값인 4가 반환된다.

![Untitled](/assets/images/union-2.png)

| node | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| value | 1 | 1 | 2 | 4 | 4 |

위의 두 집합 X, Y를 합치는 연산 Union(X,Y) 를 수행하면 아래와 같이 변환된다. 예제를 보고 이해가 잘 안된다면 코드를 보고 다시 배열 테이블을 복습해보는 것을 추천한다!

![Untitled](/assets/images/union-1.png)

| node | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| value | 1 | 2 | 3 | 4 | 5 |

### Find(x)

```cpp
int find(int x) {
    if (root[x] == x) return x;
    return root[x] = find(root[x]);
}
```

### Union(x, y)

```cpp
void Union(int x, int y) {
    x = find(x), y = find(y);
    if (x == y) return;
    root[y] = x;
}
```

find 연산은 해당 원소의 대표값을 반환하기 때문에 **find(x) != find(y)** 수식으로 쉽게 서로소 집합을 판별해 볼 수 있다.
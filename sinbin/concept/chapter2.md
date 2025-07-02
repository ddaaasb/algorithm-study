## 알고리즘의 **특성**

1. **정확성**
    - 주어진 문제에 대해 올바른 해를 주어야 한다,
2. **수행성**
    - 각 단계는 컴퓨터에서 수행 가능해야 한다.
3. **유한성**
    - 일정한 시간 내에 종료되어야 한다.
4. **효율성**
    - 효율적일 수록 그 가치가 높다.

---

## 알고리즘의 분류

1. **분할 정복 (Divide and Conquer)**
2. **그리디 (Greedy)**
3. **동적 계획법 (Dynamic Programming)**
4. **근사 (Approximation)**
5. **백트래킹 (Backtracking)**
6. **분기 한정 (Branch and Bound)**

---

### 그 알고리즘 유형

1. **랜덤(Randomized)**
2. **병렬(Parallel)**
3. **분산(Distributed**
4. **양자(Quantum**
5. **유전자(Genetic)**

---

## 문제 기반 알고리즘 분류

- **정렬 알고리즘**: 버블, 선택, 삽입, 병합, 퀵, 힙 정렬 등
- **그래프 알고리즘**: BFS, DFS, 다익스트라 등
- **기하 알고리즘**

---

## 알고리즘의 효율성 표현

### 시간 복잡도 (Time Complexity)

- 알고리즘이 **입력 크기 N에 대해 수행하는 연산 횟수**
- 보통 **점근적 표기법 (Asymptotic Notation)** 사용

| 표기법 | 의미 |
| --- | --- |
| **Big-O (O)** | **최악**의 경우 연산 수 (상한) |
| **Big-Ω (Omega)** | **최선**의 경우 연산 수 (하한) |
| **Big-Θ (Theta)** | 평균적/정확한 **상한과 하한이 일치** |

> 실무에선 보통 Big-O (최악 시간 복잡도) 를 사용함
> 

---

### 공간 복잡도 (Space Complexity)

- 알고리즘이 사용하는 **추가 메모리 양**을 입력 크기 N에 따라 분석
38. 임의의 숫자를 찾기 위한 순차 탐색을 의사 코드로 표현해라

```c
function liner_search(arr, target):
    for i from 0 to length(arr) - 1:
        if arr[i] == target:
            return i
    return -1
```

39. 정렬된 숫자 들에서 임의의 숫자를 찾기 위한 보간 탐색을 의사 코드로 표현하라

```c
int interpolation_search(int arr[], int n, int key) {
int comparisons = 0;
int low = 0, high = n - 1;

while (low <= high && key >= arr[low] && key <= arr[high]) {
    comparisons++;
    int pos = low + ((double)(high - low) / (arr[high] - arr[low])) * (key - arr[low]);

    if (arr[pos] == key) {
        return pos;
    }

    if (arr[pos] < key) {
        low = pos + 1;
    } else {
        high = pos - 1;
    }
}
return -1;
}

```

40. 정렬된 숫자 들에서 임의의 숫자를 찾기 위한 이진 탐색 알고리즘을 의사 코드로 표현해라

```c
function binarySearch(arr, target):
    low = 0
    high = length(arr) - 1

    while low <= high:
        mid = (low + high) 

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    return -1

```

41. 한붓그리기 문제를 해결하는 알고리즘을 의사코드로 표현해라

```c
function 한붓그리기(Graph G) {
    Stack stack;
    List path;
    int odd_count = 0;
    int start = -1;

    // 차수가 홀수인 정점 수 계산
    for (int v = 0; v < G.numVertices; v++) {
        if (G.degree[v] % 2 != 0) {
            odd_count++;
            start = v;  // 홀수 차수 정점 중 하나를 시작점으로 설정
        }
    }

    // 시작점 선택
    if (odd_count == 0) {
        for (int v = 0; v < G.numVertices; v++) {
            if (G.degree[v] > 0) {
                start = v;
                break;
            }
        }
    } else if (odd_count != 2) {
        printf("No Eulerian Path\n");
        return;
    }

    initStack(&stack);
    initList(&path);
    push(&stack, start);

    while (!isEmpty(stack)) {
        int v = top(stack);
        if (hasUnusedEdge(G, v)) {
            int u = getAnyUnusedNeighbor(G, v);
            removeEdge(G, v, u);  // 간선을 사용 처리
            push(&stack, u);
        } else {
            int popped = pop(&stack);
            append(&path, popped);
        }
    }

    reverse(&path);
    printList(path);
}

```
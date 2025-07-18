# CHAPTER3

# 분할정복

1. 분할정복 알고리즘이란?
    1. 개념
        1. 주어진 문제의 입력을 분할하여 문제를 해결(정복)하는 방식의 알고리즘
    2. 적용방식
        1. 분할된 입력에 대해 동일한 알고리즘 적용 —> 해를 계산
        2. 해를 취합하여 원래 문제의 해를 얻음
        3. 부분문제 : 분할된 입력에 대한 문제
            1. 더이상 분할할 수 없을 때까지 계속 반복
    3. 분할정복 알고리즘의 분류 —> 분할되는 부분문제의 수와 크기에 따라 분류
        1. 문제가 a개로 분할되고, 부분문제의 크기가 1/b로 감소하는 알고리즘
            1. 종류
                1. a=b=2
                    1. 합병정렬
                    2. 최근접 점의 쌍 찾기
                    3. 공제선 문제
                2. a=3, b=2
                    1. 큰 정수의 곱셈
                3. a=4, b=2
                    1. 큰 정수의 곱셈
                4. a=7, b=2
                    1. 스트라센(Strassen)의 행렬 곱셈 알고리즘
        2. 문제가 2개로 분할되고, 부분문제의 크기가 일정하지 않은 크기로 감소하는 알고리즘
            1. 종류
                1. 퀵정렬
        3. 문제가 2개로 분할되나, 그중에 1개의 부분문제는 고려할 필요 없으며, 부분문제의 크기가 1/2로 감소하는 알고리즘
            1. 종류
                1. 이진탐샘
        4. 문제가 2개로 분할되나, 그중에 1개의 부분문제는 고려할 필요 없으며, 부분문제의 크기가 일정하지 않은 크기로 감소하는 알고리즘
            1. 종류
                1. 선택 문제 알고리즘
        5. 부분문제의 크기가 1, 2개씩 감소하는 알고리즘
            1. 종류
                1. 삽입정렬
                2. 피보나치 수의 계산

# 합병 정렬

1. 합병정렬이란?
    1. 입력이 2개의 부분문제로 분할되고 부분문제의 크기가 1/2로 감소하는 분할 정복 알고리즘
2. 적용방식
    1. n개의 숫자들을 n/2개씩 2개의 부분문제로 분할
    2. 부분문제를 순환적으로 합병 정렬
    3. 2개의 정렬 부분을 합병하여 정렬(정복)
3. 시간복잡도
    1. (층수)*$O(n) = \log_{2}{8}*O(n) = O(n \log_{n})$
4. 공간복잡도
    1. $O(n)$
    2. 입력 배열(입력을 위한 메모리 공간)외의 입력과 같은 크기의 임시배열이 별도 필요
        1. 정렬된 부분을 합병할때 결과 저장 공간이 필요하기 때문
5. 장점 및 사용
    1. 장점
        1. 외부 정렬의 기본
        2. 연결리스트 데이터 정렬시 효율적
    2. 사용
        1. 멀티코어 CPU, 다수의 프로세서로 구성된 그래픽 처리 장치 —> 정렬 알고리즘 병렬화 사용
- 합병
    - 2개의 각각 정렬된 숫자들을 1개의 정렬된 숫자들로 합치는 것

# 퀵 정렬

분할 정복 알고리즘으로 분류되나 정복 후 분할하는 알고리즘이다.

1. 개념
    1. 문제를 2개의 부분문제로 분할하는데 부분문제의 크기가 일정하지 않은 형태의 분할 정복 알고리즘
2. 적용방식
    1. 피봇(pivot)이라 일컫는 배열의 원소(숫자)를 기준
    2. 피봇보다 큰 숫자는 오른편, 작은 숫자는 왼편에 위치하도록 분할
    3. 피봇을 그 사이에 위치
    4. 위의 과정을 순환적으로 수행
3. 알고리즘

QuickSort(A, left, right)

입력 : 배열 A[left]~A[right]

출력 : 정렬된 배열 A[left]~A[right]

if(left<right){

피봇을 A[left]~A[right] 중에서 선택하고 피봇을 A[left]와 자리를 바꾼후, 피봇과 배열의 각 원소를 비교

피봇보다 작은 숫자들은 A[left]~A[p-1]로 옮김

피봇보다 큰 숫자들은 A[p-1]~A[right]로 옮기며, 피봇은 A[p]에 놓음

QuickSort(A, left, p-1) —> 순환적 호출

QuickSort(A, p+1, right) —> 순환적 호출

}

1. 피봇 선정 방법 —> 불균형한 분할을 완화하기 위함
    1. 랜덤 선정
    2. 3 숫자의 중앙값으로 선정
        1. 가장 왼쪽 숫자, 가장 오른쪽 숫자, 중간 숫자 중에서 중앙값으로 피봇을 선정
    3. 중앙값들 중의 중앙값으로 선정
        1. 입력을 3등분
        2. 각 부분에서의 중앙값을 찾음
        3. 3개의 중앙값 중에서 중앙값을 피봇으로 설정
2. 최적화
    1. 입력 크기가 매우 클때 성능 향상
        1. 삽입정렬을 동시에 사용
            1. 부분문제의 크기가 작아지면 분할을 중단
            2. 삽입정렬 사용
3. 사용
    1. 생물 정보 공학

# 선택 문제

1. 정의
    1. n개의 숫자들 중에서 k번째로 작은 숫자를 찾는 문제
2. 방법
    1. 최소 숫자를 k번 찾는다. 단, 최소 숫자를 찾은 뒤에는 입력에서 그 숫자를 제거한다.
    2. 숫자들을 오름차순으로 정렬한 후, k번째 숫자를 찾는다.

—> 최악의 경우 $O(kn), O(n\log{n})$의 수행시간이 걸린다.

—> 효율적인 해결을 위해 분할 정복 사용

1. 효율성을 위한 이진탐색 아이디어 적용
    1. 이진탐색은 정렬된 입력의 중간 숫자와 찾고자 하는 숫자를 비교 후 입력을 1/2로 나눈 두 부분 중에 한 부분만을 검색
    2. 선택 문제는 입력이 정렬되어있지 않음 —> 입력 숫자 중에서 피봇을 선택하여 분할
    3. Small Group
        1. 피봇보다 작은 숫자의 그룹
    4. Large Group
        1. 피봇보다 큰 숫자의 그룹

—> 각 그룹의 숫자의 개수를 알아내어 k번째 작은 숫자가 어디 있는지, 그 그룹에서 몇번째 작은 숫자를 

 찾아야 하는지 알수 있음.

- Small Group에 k번째 작은 숫자가 속한 경우
    - k번째 작은 숫자를 small group에서 찾음
- Large Group에 k번째 작은 숫자가 있는 경우
    - (k-|Small Group|-1)번재로 작은 숫자를 Large Group에서 찾음
    - |Small Group| —> Small Group에 있는 수의 개수
    - 1 —> 피봇

선택 문제 알고리즘은 문제가 2개의 부분문제로 분할 

but, 1개의 부분문제는 고려할 필요 X

부분 문제의 크기가 일정하지 않은 크기로 감소하는 형태이다.

1. 시간 복잡도
    1. 아이디어
        1. 피봇을 랜덤하게 정함 —> good 분할의 확률은 1/2 —> 평균 2회 연속해서 랜덤하게 피봇을 정하면 good 분할 가능
        2. good 분할만 연속하여 이루어졌을 때만의 시간복잡도를 구함 —> *2 —> 평균 시간 복잡도
    2. 진행
        1. 처음 입력 크기가 n —> 피봇을 랜덤하게 정한후 입력은 두그룹으로 분할 —> O(n)
        2. 분할 후 큰 부분의 최대 크기 —> (3/4n-1) —> good 분할만 일어난다고 가정(편의상 3/4n으로 놓고 시작)
        3. 2번째 good 분할
            1. 큰 부분의 크기 : 3/4n —> 랜덤 피봇
            2. 그룹 분할 시간 : $O(3/4n)$
            3. 큰 리스트의 최대 크기 : $(3/4n)(3/4n) = (3/4n)^2n$
        4. 3번째 good 분할
            1. 랜덤 피봇 : $(3/4n)^2n$
            2. 그룹 분할 시간 : $O((3/4n)^2n)$
            3. 큰 부분의 최대 크기 : $(3/4n)(3/4n)^2n = (3/4n)^3n$
        5. i번째 good 분할
            1. 랜덤 피봇 : $(3/4n)^{i-1}n$
            2. 그룹 분할 시간 : $O((3/4n)^{i-1}n)$
            3. 큰 부분의 최대 크기 : $(3/4n)(3/4n)^2n = (3/4n)^in$
        6. i번째 까지 모두 더하면 O(n)
        7. *2를 하면 O(n)
2. 사용
    1. 데이터 분석을 위한 중앙값 찾는데 사용

# 최근접 점의 쌍 찾기

1. 개념 
    1. 2차원 평면상의 n개의 점이 입력으로 주어질 때, 거리가 가장 가까운 한 쌍의 점을 찾는 문제
2. 구하는 방법
    1. 모든점에 대해 각각의 두 점 사이의 거리 계산하여 가까운 점 찾기 —> 시간 복잡도 : $O(n^2)$
    2. 비효율적이라는 문제 —> 분할 정복을 이용
3. 아이디어
    1. n개의 점을 1/2로 분할
    2. 부분 문제에서 최근접 점의 쌍 찾기
    3. 2개의 부분해 중에서 짧은 거리를 가진 점의 쌍 찾기
    4. 2개의 부분 문제 사이의 점에서 최소 거리가 나올 수도 있음 —> 일정 거리 사이에도 최근접 쌍이 있는 지 확인 필요
4. 시간복잡도
    1. 입력 : S
    2. 입력 개수 : n
    3. 전처리 과정으로서 S의 점을 x-좌표로 정렬하는 시간 : $O(n\log{n})$
    4. 알고리즘 식(3.4절 알고리즘 파트 참조) Line1에서 $O(1)$의 시간 소요
    5. Line 2에서는 S를 R, L로 분할  —> $O(1)$
    6. Line 3~4에서 L과 R에 대해 각각 ClosetPair 호출 —> 합병 정렬과 동일
    7. Line 5에서 $d= min(dist(CP_{L}, dist(CP_{R}))$일 때 중간 영역에 속하는 점들 중 최근접 쌍 찾기
        1. 중간 영역 y-좌표 기준으로 정렬 —> $O(n\log{n})$
        2. 아래에서 위 또는 점 기준으로 거리 계산 —> $O(1)$
        3. 최종 $O(n\log{n})$시간이 걸림
    8. Line 6 —> $O(1)$
    9. 총 k( $\log{n}$ )층까지 분할  —> 층별로 line 5~6이 수행
    10. 최종 : $O(n\log{n})*\log{n} = O(n\log^2{n})$

시간 복잡도 최적화

—> line 5수행시 y-좌표 기준으로 중간 영역 점 정렬로 인한 시간 증가

—> 전처리 과정에서 미리 y-좌표 기준으로 정렬

1. 사용
    1. 컴퓨터 그래픽스
    2. 컴퓨터 비전
    3. 지리 정보 시스템
    4. 분자 모델링
    5. 항공 트래픽 제어
    6. 마케팅

# 분할 정복을 적용하는 데 있어서 주의할 점

1. 분할 정복이 부적절한 경우
    1. 분할될 때마다 분할된 부분 문제의 입력 크기의 합이 분할되기 전의 입력 크기보다 매우 커지는 경우
    2. 취합(정복) 과정 유의
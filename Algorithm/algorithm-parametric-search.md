# 파라메트릭 서치 (Parametric Search)

## 1. 파라메트릭 서치란?
- 파라메트릭 서치는 최적화 문제를 결정 문제로 바꾸어 풀어 나가는 기법입니다.
- 결정 문제는 'yes' or 'no', 즉, '예' 또는 '아니오'로 답하는 문제입니다.
- 파라메트릭 서치는 주로 특정 조건을 만족하면서 동시에 가장 적합한 변숫 값을 찾아나가는 문제에서 활용되며, [이진 탐색(Binary Search)](link)을 이용하여 구현합니다.
- 예: 특정 조건을 만족하는 가장 큰 값을 구하는 최적화 문제에서 이진 탐색을 통해 적합한 해(solution)의 범위를 절반씩 좁혀 나갈 수 있습니다.

## 2. 파라메트릭 서치는 언제 사용하면 좋을까?
- 이진 탐색 알고리즘은 입력 데이터가 많거나(e.g., 1,000만 개 이상) 탐색 범위의 크기가 매우 넓을 때(e.g., 1,000억 이상) 효율적으로 문제를 해결할 수 있습니다.
- 파라메트릭 서치 역시 이와 같은 상황에서 사용하면 좋습니다.

## 3. 파라메트릭 서치와 이진 탐색 간의 차이점
- 파라메트릭 서치와 이진 탐색 간의 주요 차이점은 결정 문제냐 아니냐입니다.
- 파라메트릭 서치는 특정 조건을 만족하는 해(solution)를 찾을 때 결정 문제를 통해 접근합니다.

## 4. 파라메트릭 서치 동작 과정
이제 파라메트릭 서치의 동작 과정에 대해 알아봅니다.
파라메트릭 서치는 이분 탐색을 기반으로 구현하기 때문에,
리스트 내 특정 값을 찾기 위해 시작 인덱스, 중간 인덱스, 마지막 인덱스를 사용합니다. 구체적인 동작 순서는 아래와 같습니다.

1️⃣ 시작 인덱스와 마지막 인덱스 사이의 중간 값에서 소수점 이하를 버려 중간 인덱스를 정합니다.

2️⃣ 중간 인덱스에 해당하는 값을 활용했을 때 문제에서 주어진 조건을 만족하는지 여부를 확인합니다. 조건에 만족하지 않는다면 시작 인덱스 또는 마지막 인덱스를 수정하여 조건을 만족하는 중간 인덱스를 구합니다.

3️⃣ 조건을 만족한다면 2️⃣에서 구한 값이 최적의 해인지 여부를 확인합니다. 최적의 해라면 동작을 중단합니다.

4️⃣ 문제에서 주어진 조건을 만족하며 최적의 해를 구할 때까지 1️⃣~ 3️⃣ 과정을 반복합니다.

### 4.1. 파라메트릭 서치 예시

예를 들어, 아래 ***그림 1***
 과 같이 사람마다 고유 번호가 있는 10명의 사람이 성적에 따라 오름차순 정렬되어 있다고 가정해 보겠습니다. 여기서 "학점이 A(4.0) 이상"을 결정 문제의 조건이라고 하겠습니다. 해당 조건인 A 학점을 받은 사람 중 성적이 가장 낮은 사람을 찾는 문제를 파라메트릭 서치 기법으로 풀어보겠습니다.

![image](https://github.com/Study-Nine/StudyNine_CS/assets/54762273/3f057eb6-3782-48e5-8d88-827f44919e81)

(1) 먼저 시작점인 1과 끝점인 10의 중간점은  (1 + 10) / 2 = 5.5 에서 소수점 이하를 버린 5입니다.

 중간점이 조건을 만족하는지 확인합니다(***그림 2***참고). 

편의상 **시작점**과 **끝점**은 **녹색**으로, **중간점**은 **파란색**으로 표현하겠습니다. 

중간점인 5가 조건을 만족하지 않는다면, 이미 1부터 10번까지의 사람이 성적 순으로 정렬되어 있다는 점에서, 사실상 5번을 포함해 번호가 낮은 사람들에 대해서는 조건의 만족 여부를 검증해 볼 필요가 없습니다.

![image](https://github.com/Study-Nine/StudyNine_CS/assets/54762273/6ce90a34-ba22-4daa-bda3-22e675877692)

(2) 아래의 ***그림 3*** 과 같이 **검증이 불필요한 사람**은 **회색**으로 표현하겠습니다. 

이제 시작점은 6, 끝점은 여전히 10이기 때문에 중간점은 8이 됩니다.

이번에는 중간점 8번 사람이 학점이 A 이상이라고 답했습니다. 따라서 끝 점은 중간 점 한 칸 앞인 7이 됩니다.

![image](https://github.com/Study-Nine/StudyNine_CS/assets/54762273/5afd4f9a-c8d8-49e1-bda5-a81311d8dff2)

(3) 마찬가지로 8번 사람이 A 학점 이상이며 9번, 10번 사람은 8번 사람보다도 성적이 높기 때문에 8반 사람 이후로는 학점을 물어보지 않아도 됩니다(***그림 4*** 참고). 

이제 끝점을 중간점의 한 칸 앞인 7로 옮기면 새로운 중간점은 시작점과 같은 6이 됩니다. 

중간점에 해당하는 사람이 A 학점 이상이라고 답했기 때문에, A 학점이면서 성적이 가장 낮은 사람은 6번 사람임을 알 수 있습니다.

만일 6번이 A 학점이 아닐 경우에는 7번 사람의 학점도 알 수 없기 때문에 한 번 더 학점을 물어봐야 합니다.
### 4.2. 파라메트릭 서치의 시간 복잡도
이진 탐색은 시간 복잡도가 O(logN)입니다. 파라메트릭 서치 역시 O(logN)의 시간 복잡도를 갖습니다.

### 4.2. 파라메트릭 서치의 시간 복잡도

이진 탐색은 시작, 중간, 끝 인덱스를 활용하며 탐색 횟수 별로 확인하는 데이터의 개수가 절반씩 줄어들기 때문에 시간 복잡도가 ***O(logN)*** 입니다. 마찬가지로 파라메트릭 서치 역시 ***O(logN)*** 의 시간 복잡도를 갖습니다.

## 파라메트릭 서치 문제
[백준 2512 (예산)](https://www.acmicpc.net/problem/2512)

![image](https://github.com/Study-Nine/StudyNine_CS/assets/54762273/0291284b-7539-4ee6-b62b-9c47dd9c1769)
![image](https://github.com/Study-Nine/StudyNine_CS/assets/54762273/fba19689-0774-4c4e-874d-8fda1a8e2f7e)


(여기에 문제 설명 이미지 추가)

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());

        StringTokenizer st = new StringTokenizer(br.readLine());

        long left = 0;
        long right = Integer.MIN_VALUE;

        int arr[] = new int[n];
        for(int i=0; i<n; i++){
            arr[i] = Integer.parseInt(st.nextToken());
            right = Math.max(arr[i], right);
        }

        long total = Integer.parseInt(br.readLine());
        while(left <= right){
            long mid = (left + right) / 2;
            long budget = 0;

            for(int i=0; i<n; i++){
                budget += (arr[i] > mid) ? mid : arr[i];
            }

            if(budget <= total) left = mid +1;
            else right = mid -1;
        }

        System.out.println(right);
    }
}

# [문제링크]()

## 📝 문제

철호는 수열을 가지고 놀기 좋아합니다. 어느 날 철호는 어떤 자연수로 이루어진 원형 수열의 연속하는 부분 수열의 합으로 만들 수 있는 수가 모두 몇 가지인지 알아보고 싶어졌습니다. 원형 수열이란 일반적인 수열에서 처음과 끝이 연결된 형태의 수열을 말합니다. 예를 들어 수열 [7, 9, 1, 1, 4] 로 원형 수열을 만들면 다음과 같습니다.  
![그림.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/f207cd37-34dc-4cbd-96bb-83435bd6efd4/%EA%B7%B8%EB%A6%BC.png)  
원형 수열은 처음과 끝이 연결되어 끊기는 부분이 없기 때문에 연속하는 부분 수열도 일반적인 수열보다 많아집니다.  
원형 수열의 모든 원소 `elements`가 순서대로 주어질 때, 원형 수열의 연속 부분 수열 합으로 만들 수 있는 수의 개수를 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 3 ≤ `elements`의 길이 ≤ 1,000
- 1 ≤ `elements`의 원소 ≤ 1,000

---

##### 입출력 예

|elements|result|
|---|---|
|[7,9,1,1,4]|18|

---

##### 입출력 예 설명

입출력 예 #1  
길이가 1인 연속 부분 수열로부터 [1, 4, 7, 9] 네 가지의 합이 나올 수 있습니다.  
길이가 2인 연속 부분 수열로부터 [2, 5, 10, 11, 16] 다섯 가지의 합이 나올 수 있습니다.  
길이가 3인 연속 부분 수열로부터 [6, 11, 12, 17, 20] 다섯 가지의 합이 나올 수 있습니다.  
길이가 4인 연속 부분 수열로부터 [13, 15, 18, 21] 네 가지의 합이 나올 수 있습니다.  
길이가 5인 연속 부분 수열로부터 [22] 한 가지의 합이 나올 수 있습니다.  
이들 중 중복되는 값을 제외하면 다음과 같은 18가지의 수들을 얻습니다.  
[1, 2, 4, 5, 6, 7, 9, 10, 11, 12, 13, 15, 16, 17, 18, 20, 21, 22]

---

### 💡 풀이

- 예제 **\[7, 9, 1, 1, 4\]** 를 가지고 규칙을 찾아보았습니다.

| 길이 | 수열                   | 비고       |
|:---- |:---------------------- |:---------- |
| 1    | 7, 9, 1, 1, 4          | length     |
| 2    | 7, 9, 1, 1, 4, 7       | length + 1 |
| 3    | 7, 9, 1, 1, 4, 7, 9    | length + 2 |
| 4    | 7, 9, 1, 1, 4, 7, 9, 1 | length + 3 |
| 5    | 7, 9, 1, 1, 4, 7, 9, 1, 1          | length + 4          |

- 배열의 요소를 하나만 가지고 수열을 만든다고 할 때는 배열 그대로만 사용하면 됩니다.
- 배열의 요소를 2개를 더해서 수열을 만든다고 하면 7, 9, 1, 1, 4에서 7+9, 9+1, 1+1, 1+4 가 가능하지만 문제에서는 원형 배열로 정의하고 있기 때문에 4+7 또한 가능합니다. 따라서 원형 배열을 일자로 나열한다고 가정하면 7, 9, 1, 1, 4, 7(0번 인덱스) 가 되어야 하는 것입니다.
- 배열의 요소 3개를 더한다고 하면 7+9+1, 9+1+1, 1+1+4 이고 원형 배열이므로  1+4+7, 4+7+9 또한 가능합니다. 다시 원형 배열을 일자로 나열해보면 7, 9, 1, 1, 4, 7(0번 인덱스), 9(12번 인덱스) 가 되겠죠!
- 규칙대로라면 더하는 요소의 개수에 따라 길이가 **length + (더하는 요소의 개수-1)** 가 된다는 것을 알 수 있습니다!
- **요소의 길이는 1부터 배열의 길이까지** 순차적으로 계산해야 하므로 첫 번째 for문은 아래와 같습니다.

```java
for (int i = 1; i < elements.length; i++) {}
```

- 그리고 각 요소의 길이(i)마다 연산은 elements의 길이만큼 하게 됩니다.
- 예를 들어서 길이가 1일 때는 7, 9, 1, 1, 4를 각각 한 번씩 총 5번 탐색하게 되고, 길이가 2일 때는 7+9, 9+1, 1+1, 1+4, 4+7 로 똑같이 총 5번 탐색하게 됩니다. 

```java
for (int i = 1; i <= elements.length; i++) {
	for (int j = 0; j < elements.length; j++) {
}
```

- 그리고 각각의 요소를 더해서 HashSet에 넣어주는 작업을 해야겠죠?!
- 요소의 길이(i) 만큼을 더해주어야 하므로 세 번째 for문은 아래와 같습니다.

```java
for (int i = 1; i <= elements.length; i++) {
	for (int j = 0; j < elements.length; j++) {
		int sum = 0;          
		for (int k = j; k < j+i; k++) {
		}
	}
```

- 그리고 sum을 해주어야 하는데 **j+i**를 하게 되면 elements의 길이를 넘어가게 되고 우리는 길이가 넘어가게 되면 다시 0번 인덱스로 돌아가는 작업을 해주어야 합니다.
- 7, 9, 1, 1, 4 라는 배열만을 가지고 7, 9, 1, 1, 4, 7, 9 를 만들어낼 수 있어야 하죠!
- 4번 인덱스인 4 다음에 0번 인덱스 7이 나오도록 하려면 어떻게 해야 할까요?
- 이것은 나머지 연산으로 계산이 가능합니다!
- 4번 인덱스 다음이 5가 되는데 이것을 배열의 길이로 나머지 계산을 해주면 됩니다.
	- 1 % 5 = 1
	- 2 % 5 = 2
	- 3 % 5 = 3
	- 4 % 5 = 4
	- 5 % 5 = 0
	- 6 % 5 = 1
	- 7 % 5 = 2
- 이런 식으로 배열의 길이만큼 인덱스가 순환하는 구조가 만들어집니다.
- 마지막으로 연산한 것들을 set에 넣어주고 set의 길이를 리턴해주면 되는데 저같은 경우는 배열의 길이가 5이고 요소 5개를 더하는 연산의 경우 7+9+1+1+4, 9+1+1+4+7, 1+1+4+7+9 ... 이런식으로 계산이 되는데, 어차피 같은 수를 계속 연산하고 있죠?!
- 모든 요소의 수를 더하는 것은 이전에 중복해서 나올 수 없는 수이고, 또한 set에서 걸러지긴 하지만 의미없는 연산이 되기 때문에 roop에서 제외하고 set.size() + 1 을 리턴해주는 식으로 구현하였습니다.

```java
for (int i = 1; i <= elements.length; i++) {
	...
	return set.size();
}

for (int i = 1; i < elements.length; i++) {}
	...
	return set.size() + 1;
```


### 🔍 정답

```java
import java.util.*;

class Solution {
    public int solution(int[] elements) {
        HashSet<Integer> set = new HashSet<>();
        
        // 연산 길이: 1부터 elements 길이까지
        for (int i = 1; i < elements.length; i++) {
            
            // 매 연산 길이당 elements 길이만큼 반복
            for (int j = 0; j < elements.length; j++) {
                int sum = 0;          
                
                // 연산 길이 i 만큼 sum 연산
                for (int k = j; k < j+i; k++) {
                    sum += elements[k % elements.length];
                }
                
                set.add(sum);
            }       
        }
    
        return set.size() + 1;
    }
}
```
# [λ¬Έμ λ§ν¬](https://www.acmicpc.net/problem/10819)

## π λ¬Έμ 

Nκ°μ μ μλ‘ μ΄λ£¨μ΄μ§ λ°°μ΄ Aκ° μ£Όμ΄μ§λ€. μ΄λ, λ°°μ΄μ λ€μ΄μλ μ μμ μμλ₯Ό μ μ ν λ°κΏμ λ€μ μμ μ΅λκ°μ κ΅¬νλ νλ‘κ·Έλ¨μ μμ±νμμ€.

|A[0] - A[1]| + |A[1] - A[2]| + ... + |A[N-2] - A[N-1]|

## μλ ₯

μ²«μ§Έ μ€μ N (3 β€ N β€ 8)μ΄ μ£Όμ΄μ§λ€. λμ§Έ μ€μλ λ°°μ΄ Aμ λ€μ΄μλ μ μκ° μ£Όμ΄μ§λ€. λ°°μ΄μ λ€μ΄μλ μ μλ -100λ³΄λ€ ν¬κ±°λ κ°κ³ , 100λ³΄λ€ μκ±°λ κ°λ€.

## μΆλ ₯

μ²«μ§Έ μ€μ λ°°μ΄μ λ€μ΄μλ μμ μμλ₯Ό μ μ ν λ°κΏμ μ»μ μ μλΒ μμ μ΅λκ°μ μΆλ ₯νλ€.

## μμ  μλ ₯ 1Β 

6
20 1 15 8 4 10

## μμ  μΆλ ₯ 1Β 

62


---

### π μ λ΅

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    static int N;
    static int max = 0;
    static int[] arr, newArr;
    static boolean[] visit;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        arr = new int[N]; // μλ ₯κ°μ λ΄μ λ°°μ΄
        newArr = new int[N]; // μμλ€μ μ¬μ‘°ν©ν΄μ λ΄μ λ°°μ΄
        visit = new boolean[N]; // λ°©λ¬Έ μ¬λΆλ₯Ό μ²΄ν¬ν  λ°°μ΄
        StringTokenizer st = new StringTokenizer(br.readLine());

        /* μλ ₯κ°μ λ΄λλ€! */
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        dfs(0);
        System.out.println(max);
    }

    public static void dfs(int cnt) {
        /* λ°°μ΄μ΄ λͺ¨λ λ΄κΈ°λ©΄ calculate()λ‘ κ³μ°μ νκ³  κ³μ°κ°μ maxμ λΉκ΅νμ¬ κ°±μ ν΄μ€λ€! */
        if (cnt == N) {
            max = Math.max(calculate(), max);
            return;
        }

        /**
         * μμ΄μ μ΄μ©νμ¬ μ€λ³΅μ μ μΈνκ³  λͺ¨λ  μμλ₯Ό κ³ λ €ν κ²½μ°μ μλ₯Ό κ³μ°ν΄λ³Έλ€
         */
        for (int i = 0; i < N; i++) {
            if (!visit[i]) {
                visit[i] = true;
                newArr[cnt] = arr[i];
                dfs(cnt + 1);
                visit[i] = false;
            }
        }
    }

    /* μ£Όμ΄μ§ λ¬Έμ μ μμ μ΄μ©ν΄ κ³μ°ν λ©μλ! */
    public static int calculate() {
        int answer = 0;
        for (int i = 0; i < N-1; i++) {
            answer += Math.abs(newArr[i] - newArr[i+1]);
        }
        return answer;
    }
}
```


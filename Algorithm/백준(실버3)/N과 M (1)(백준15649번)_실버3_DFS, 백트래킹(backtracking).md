# [๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/15649)

## ๐ ๋ฌธ์ 

์์ฐ์ N๊ณผ M์ด ์ฃผ์ด์ก์ ๋, ์๋ ์กฐ๊ฑด์ ๋ง์กฑํ๋ ๊ธธ์ด๊ฐ M์ธ ์์ด์ ๋ชจ๋ ๊ตฌํ๋ ํ๋ก๊ทธ๋จ์ ์์ฑํ์์ค.

-   1๋ถํฐ N๊น์งย ์์ฐ์ ์ค์์ ์ค๋ณต ์์ด M๊ฐ๋ฅผ ๊ณ ๋ฅธ ์์ด

## ์๋ ฅ

์ฒซ์งธ ์ค์ ์์ฐ์ N๊ณผ M์ด ์ฃผ์ด์ง๋ค. (1 โค M โค N โค 8)

## ์ถ๋ ฅ

ํ ์ค์ ํ๋์ฉ ๋ฌธ์ ์ ์กฐ๊ฑด์ ๋ง์กฑํ๋ ์์ด์ ์ถ๋ ฅํ๋ค. ์ค๋ณต๋๋ ์์ด์ ์ฌ๋ฌ ๋ฒ ์ถ๋ ฅํ๋ฉด ์๋๋ฉฐ, ๊ฐ ์์ด์ ๊ณต๋ฐฑ์ผ๋ก ๊ตฌ๋ถํด์ ์ถ๋ ฅํด์ผ ํ๋ค.

์์ด์ ์ฌ์  ์์ผ๋ก ์ฆ๊ฐํ๋ ์์๋ก ์ถ๋ ฅํด์ผ ํ๋ค.

## ์์  ์๋ ฅ 1

3 1

## ์์  ์ถ๋ ฅ 1ย 

1
2
3

## ์์  ์๋ ฅ 2ย 

4 2

## ์์  ์ถ๋ ฅ 2ย 

1 2
1 3
1 4
2 1
2 3
2 4
3 1
3 2
3 4
4 1
4 2
4 3

## ์์  ์๋ ฅ 3ย 

4 4

## ์์  ์ถ๋ ฅ 3ย 

1 2 3 4
1 2 4 3
1 3 2 4
1 3 4 2
1 4 2 3
1 4 3 2
2 1 3 4
2 1 4 3
2 3 1 4
2 3 4 1
2 4 1 3
2 4 3 1
3 1 2 4
3 1 4 2
3 2 1 4
3 2 4 1
3 4 1 2
3 4 2 1
4 1 2 3
4 1 3 2
4 2 1 3
4 2 3 1
4 3 1 2
4 3 2 1


---

### ๐ ์ ๋ต

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.StringTokenizer;  
  
public class Main {  
  
    public static int[] arr;  
    public static boolean[] visit;  
    public static int N;  
    public static int M;  
  
    public static StringBuilder sb = new StringBuilder();  
    public static void main(String[] args) throws IOException {  
  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
  
        StringTokenizer st = new StringTokenizer(br.readLine());  
  
        N = Integer.parseInt(st.nextToken());  
        M = Integer.parseInt(st.nextToken());  
  
        arr = new int[M];  
        visit = new boolean[N+1];  
        dfs(0);  
        System.out.println(sb);  
  
    }  

    public static void dfs(int depth) {  
        if (depth == M) {  
            for (int val : arr) {  
                sb.append(val).append(' ');  
            }  
            sb.append('\n');  
            return;  
        }  

        for (int i = 1; i <= N; i++) {  
            if (!visit[i]) {  
                visit[i] = true;  
                arr[depth] = i;  
                dfs(depth + 1);  
                visit[i] = false;  
            }  
        }  
    }  
}
```
- ๊ธฐ๋ณธ ๋ฐฑํธ๋ํน ๋ฌธ์ ๋ก dfs๋ฅผ ์ด์ฉํด ํ์ด์ผ ํ๋ ๋ฌธ์ ์ด๋ค.
- ํ์ด๋ฅผ ๋ด๋๋ด๋ ์ดํด๊ฐ ์ ๊ฐ์ ๋ธ๋ก๊ทธ ๊ธ์ ๋๋ถ๋ถ ๋ค ๋ณธ ๊ฒ ๊ฐ๊ณ  ์ ํ๋ธ์์๋ ๋ณด๊ณ  ์ง์  ์์ผ๋ก ๊ทธ๋ ค๋ณด๋ฉฐ ๊ฒจ์ฐ ์ด๋ ดํ์ด ์ดํดํ ๊ฒ ๊ฐ๋ค.
	- [์ ํ๋ธ ์ฐธ๊ณ ์๋ฃ](https://www.youtube.com/watch?v=Enz2csssTCs&t=684s)
- ๋ด์ฉ์ ๋ณต์ตํ  ๊ฒธ ์ ๋ฆฌํด๋ณด๋ ค๊ณ  ํ๋ค ใ ใ 
- ์ ๋ฆฌํ  ๋ ์ฌ์ฉํ๋ ์์์ ๋ด์ฉ์ N=4, M=2๋ก ์ ํ๊ณ  ์งํํ๊ธฐ๋ก ํ๋ค.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4oGNT%2FbtrRX1mdVW7%2FYxISK97R1hXoQfoXYg5Nak%2Fimg.jpg)
- ๊ธฐ๋ณธ ํ์ ์ด๋ฌํ ํธ๋ฆฌ๊ตฌ์กฐ์ด๋ค
- dfs(0) : i = 1, depth = 0
- dfs(1) : arr[0] = 1 ๋ถํฐ ์์
- dfs(2) : arr[1]์ 2๋ก ์ฑ์ฐ๊ณ  ๋ฆฌํด(dfs(1)), 3์ผ๋ก ์ฑ์ฐ๊ณ  ๋ฆฌํด(dfs(1)), 4๋ก ์ฑ์ฐ๊ณ  ๋ฆฌํด(dfs(1))
- ๋ชจ๋  ์๋ฅผ ๋์์ผ๋ฉด depth 1 ์์ depth 0์ผ๋ก ๋์๊ฐ์ i = 2 ๋ก ์ ๋ด์ฉ์ ๋ฐ๋ณตํ๋ค

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPhmmB%2FbtrRXD0fEvk%2FX4wPepKjboUjF26CXOlKL1%2Fimg.jpg)
- ๋ค์ ์์ผ๋ก ์จ๋ณด๋ฉด์ ์ฐจ๊ทผ์ฐจ๊ทผ ์์๋ฅผ ์๊ฐํด๋ณด์!
- N, M์ ์๋ ฅ๋ฐ๊ณ  ์ถ๋ ฅ์ ์ํ arr ๋ฐฐ์ด๊ณผ, ๋ฐฉ๋ฌธ์ฌ๋ถ๋ฅผ ๊ฐ๋ฆด visit ๋ฐฐ์ด์ ์ ์ญ๋ณ์๋ก ์ ์ธ
	- visit = [F F F F F] (ํธ์์ 0๋ฒ ์ธ๋ฑ์ค๋ ์๊ฐํ์ง ์์ ์์ )
	- arr = [0 0]
- dfs(0) ํธ์ถ
	- depth == M ์ด ์๋๋ฏ๋ก ์๋ for๋ฌธ์ผ๋ก ์ด๋
	- i = 1, depth = 0
	- visit = [T F F F]
	- arr = [1 0]
	- dfs(1) ํธ์ถ === ์ฒ์ dfs(1)์ ํธ์ถํ ๊ณณ ===
		- depth == M ์ด ์๋๋ฏ๋ก ์๋ for๋ฌธ์ผ๋ก ์ด๋
		- i = 1์ True์ด๋ฏ๋ก i = 2๋ถํฐ ์์, depth = 1
		- visit = [T T F F]
		- arr = [1 2]
		- dfs(2) ํธ์ถ (return ๋๋ฉด ๋์์ค๋ ๊ณณ)
			- depth == M ์ด๋ฏ๋ก sb์ ๊ฐ ์ ์ฅ([1, 2]) ํ return
		- return ๋ dfs(1)
			- return ๋์์ผ๋ฏ๋ก dfs(2)๋ฅผ ํธ์ถํ๋ ๋ค์ ์ค ์คํ
			- i = 2์์ผ๋ฏ๋ก visit[2] = false, visit = [T F F F]
			- i = 3, depth = 1 (i = 2๊น์ง ์งํํ์์ผ๋ฏ๋ก)
			- visit = [T F T F]
			- arr = [1 3]
			- dfs(2) ํธ์ถ (return ๋๋ฉด ๋์์ค๋ ๊ณณ)
				- depth == M ์ด๋ฏ๋ก sb์ ๊ฐ ์ ์ฅ([1, 3]) ํ return
		- return ๋ dfs(1)
			- return ๋์์ผ๋ฏ๋ก dfs(2)๋ฅผ ํธ์ถํ๋ ๋ค์ ์ค ์คํ
			- i = 3 ์ด์์ผ๋ฏ๋ก visit[3] = falst, visit = [T F F F]
			- i = 4, depth = 1
			- visit = [T F F T]
			- arr = [1 4]
			- dfs(2) ํธ์ถ (return ๋๋ฉด ๋์์ค๋ ๊ณณ)
				- depth == M ์ด๋ฏ๋ก sb์ ๊ฐ ์ ์ฅ([1, 4]) ํ return
		- return ๋ dfs(1)
			- return ๋์์ผ๋ฏ๋ก dfs(2)๋ฅผ ํธ์ถํ๋ ๋ค์ ์ค ์คํ
			- i = 4 ์์ผ๋ฏ๋ก visit[4] = false, visit = [T F F F]
			- for๋ฌธ์ด ์ข๋ฃ๋์์ผ๋ฏ๋ก dfs(1)์ ์ฒ์ ํธ์ถํ ๊ณณ์ผ๋ก ๋์๊ฐ๊ธฐ
	- ์ฒ์ dfs(1)์ ํธ์ถํ ๊ณณ์ผ๋ก ๋์์์ ๋ค์ ์ค ์คํ
	- i = 1์ด์์ผ๋ฏ๋ก visit[1] = false, visit = [F F F F]

	- i = 2, depth = 0 ์ผ๋ก i <= N ์ผ ๋๊น์ง ์ ๋ด์ฉ์ ๋ฐ๋ณตํ๊ฒ ๋๋ค!
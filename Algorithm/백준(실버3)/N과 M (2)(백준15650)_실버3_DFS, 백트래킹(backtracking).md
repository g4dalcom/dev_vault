# [๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/15650)

## ๐ ๋ฌธ์ 

์์ฐ์ N๊ณผ M์ด ์ฃผ์ด์ก์ ๋, ์๋ ์กฐ๊ฑด์ ๋ง์กฑํ๋ ๊ธธ์ด๊ฐ M์ธ ์์ด์ ๋ชจ๋ ๊ตฌํ๋ ํ๋ก๊ทธ๋จ์ ์์ฑํ์์ค.

-   1๋ถํฐ N๊น์งย ์์ฐ์ ์ค์์ ์ค๋ณต ์์ด M๊ฐ๋ฅผ ๊ณ ๋ฅธ ์์ด
-   ๊ณ ๋ฅธ ์์ด์ ์ค๋ฆ์ฐจ์์ด์ด์ผ ํ๋ค.

## ์๋ ฅ

์ฒซ์งธ ์ค์ ์์ฐ์ N๊ณผ M์ด ์ฃผ์ด์ง๋ค. (1 โค M โค N โค 8)

## ์ถ๋ ฅ

ํ ์ค์ ํ๋์ฉ ๋ฌธ์ ์ ์กฐ๊ฑด์ ๋ง์กฑํ๋ ์์ด์ ์ถ๋ ฅํ๋ค. ์ค๋ณต๋๋ ์์ด์ ์ฌ๋ฌ ๋ฒ ์ถ๋ ฅํ๋ฉด ์๋๋ฉฐ, ๊ฐ ์์ด์ ๊ณต๋ฐฑ์ผ๋ก ๊ตฌ๋ถํด์ ์ถ๋ ฅํด์ผ ํ๋ค.

์์ด์ ์ฌ์  ์์ผ๋ก ์ฆ๊ฐํ๋ ์์๋ก ์ถ๋ ฅํด์ผ ํ๋ค.

## ์์  ์๋ ฅ 1ย 

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
2 3
2 4
3 4

## ์์  ์๋ ฅ 3ย 

4 4

## ์์  ์ถ๋ ฅ 3ย 

1 2 3 4


---

### ๐ ๋์ ์ ๋ต

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.StringTokenizer;  
  
public class Main {  
    public static int N;  
    public static int M;  
    public static int[] array;  
    public static boolean[] visit;  
    public static StringBuilder sb = new StringBuilder();  
  
    public static void main(String[] args) throws IOException {  
  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        StringTokenizer st = new StringTokenizer(br.readLine());  
        N = Integer.parseInt(st.nextToken());  
        M = Integer.parseInt(st.nextToken());  
  
        array = new int[M];  
        visit = new boolean[N];  
        dfs(0);  
        System.out.println(sb);  
    }  
  
    public static void dfs(int depth) {  
        if (depth == M) {  

			/* ์ถ๊ฐ๋ ๋ถ๋ถ */ 
            int max = array[0];  
            for (int i = 1; i < M; i++) {  
                if (max < array[i]) max = array[i];  
                else return;  
            }  
  
            for (int var : array) {  
                sb.append(var).append(' ');  
            }  
            sb.append("\n");  
            return;  
        }  
  
        for (int i = 0; i < N; i++) {  
            if (!visit[i]) {  
                visit[i] = true;  
                array[depth] = i + 1;  
                dfs(depth + 1);  
                visit[i] = false;  
            }  
        }  
    }  
}
```
- [[N๊ณผ M (1)(๋ฐฑ์ค15649๋ฒ)_์ค๋ฒ3_DFS, ๋ฐฑํธ๋ํน(backtracking)]]
- N๊ณผ M (1)์์ array์ ์๋ ์๊ฐ ์ค๋ฆ์ฐจ์์ผ ๋๋ง sb์ ์ ์ฅํ  ์ ์๋๋ก ์กฐ๊ฑด๋ฌธ๋ง ์ถ๊ฐํ์๋ค.
- ํ์ง๋ง ๋ฌธ์ ๋ฅผ ํ๊ณ  ๋ค๋ฅธ ์ฌ๋์ ํ์ด๋ฅผ ํ์ธํ ๊ฒฐ๊ณผ, ์ด ๋ฌธ์ ์ ์๋๋ ์์ด๊ณผ ์กฐํฉ์ ์ฐจ์ด๋ฅผ ๊ณต๋ถํ๋ผ๋ ๊ฒ์์ ์๊ฒ๋์๋ค

### ๐ ์กฐํฉ์ ์ด์ฉํ ์ ๋ต

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.io.IOException;
 
public class Main {
 
	public static int[] arr;
	public static int N, M;
	public static StringBuilder sb = new StringBuilder();
 
	public static void main(String[] args) throws IOException {
 
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
 
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
 
		arr = new int[M];
        
		dfs(1, 0);
		System.out.println(sb);
 
	}
 
	public static void dfs(int at, int depth) {
 
		if (depth == M) {
			for (int val : arr) {
				sb.append(val).append(' ');
			}
			sb.append('\n');
			return;
		}
        
		for (int i = at; i <= N; i++) {
 
			arr[depth] = i;
			dfs(i + 1, depth + 1);
 
		}
	}
}
```


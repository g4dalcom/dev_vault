# [๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/15651)

## ๐ ๋ฌธ์ 

์์ฐ์ N๊ณผ M์ด ์ฃผ์ด์ก์ ๋, ์๋ ์กฐ๊ฑด์ ๋ง์กฑํ๋ ๊ธธ์ด๊ฐ M์ธ ์์ด์ ๋ชจ๋ ๊ตฌํ๋ ํ๋ก๊ทธ๋จ์ ์์ฑํ์์ค.

-   1๋ถํฐ N๊น์งย ์์ฐ์ ์ค์์ย M๊ฐ๋ฅผ ๊ณ ๋ฅธ ์์ด
-   ๊ฐ์ ์๋ฅผ ์ฌ๋ฌ ๋ฒ ๊ณจ๋ผ๋ ๋๋ค.

## ์๋ ฅ

์ฒซ์งธ ์ค์ ์์ฐ์ N๊ณผ M์ด ์ฃผ์ด์ง๋ค. (1 โค M โค N โค 7)

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

## ์์  ์ถ๋ ฅ 2

1 1
1 2
1 3
1 4
2 1
2 2
2 3
2 4
3 1
3 2
3 3
3 4
4 1
4 2
4 3
4 4

## ์์  ์๋ ฅ 3ย 

3 3

## ์์  ์ถ๋ ฅ 3ย 

1 1 1
1 1 2
1 1 3
1 2 1
1 2 2
1 2 3
1 3 1
1 3 2
1 3 3
2 1 1
2 1 2
2 1 3
2 2 1
2 2 2
2 2 3
2 3 1
2 3 2
2 3 3
3 1 1
3 1 2
3 1 3
3 2 1
3 2 2
3 2 3
3 3 1
3 3 2
3 3 3


---

### ๐ ์ ๋ต

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.StringTokenizer;  
  
public class Main {  
    public static int N;  
    public static int M;  
    public static int[] arr;  
    public static StringBuilder sb = new StringBuilder();  
  
    public static void main(String[] args) throws IOException {  
  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        StringTokenizer st = new StringTokenizer(br.readLine());  
  
        N = Integer.parseInt(st.nextToken());  
        M = Integer.parseInt(st.nextToken());  
  
        arr = new int[M];  
        visit = new boolean[N];  
  
        dfs(0);  
        System.out.println(sb);  
    }  
  
    public static void dfs(int depth) {  
  
        if (depth == M) {  
            for (int result : arr) {  
                sb.append(result).append(' ');  
            }  
            sb.append("\n");  
            return;  
        }  
  
        for (int i = 0; i < N; i++) {  
            arr[depth] = i + 1;  
            dfs(depth + 1);  
        }  
    }  
}
```
- [[N๊ณผ M (1)(๋ฐฑ์ค15649๋ฒ)_์ค๋ฒ3_DFS, ๋ฐฑํธ๋ํน(backtracking)]]
- [[์์ด๊ณผ ์กฐํฉ]]
- ์ค๋ณต์์ด ๋ฌธ์ ๋ก, ๋ฐฉ๋ฌธ ์ฌ๋ถ๋ฅผ ๊ณ์ฐํ๋ boolean ๋ฐฐ์ด์ ์ฌ์ฉํ์ง ์์๋ค.
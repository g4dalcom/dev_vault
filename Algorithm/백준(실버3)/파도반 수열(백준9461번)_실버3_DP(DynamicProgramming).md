# [๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/9461)

## ๐ ๋ฌธ์ 

์ค๋ฅธ์ชฝ ๊ทธ๋ฆผ๊ณผ ๊ฐ์ด ์ผ๊ฐํ์ด ๋์  ๋ชจ์์ผ๋ก ๋์ฌ์ ธ ์๋ค. ์ฒซ ์ผ๊ฐํ์ ์ ์ผ๊ฐํ์ผ๋ก ๋ณ์ ๊ธธ์ด๋ 1์ด๋ค. ๊ทธ ๋ค์์๋ ๋ค์๊ณผ ๊ฐ์ ๊ณผ์ ์ผ๋ก ์ ์ผ๊ฐํ์ ๊ณ์ ์ถ๊ฐํ๋ค. ๋์ ์์ ๊ฐ์ฅ ๊ธด ๋ณ์ ๊ธธ์ด๋ฅผ k๋ผ ํ์ ๋, ๊ทธ ๋ณ์ ๊ธธ์ด๊ฐ k์ธ ์ ์ผ๊ฐํ์ ์ถ๊ฐํ๋ค.

![](https://www.acmicpc.net/upload/images/pandovan.png)

ํ๋๋ฐ ์์ด P(N)์ ๋์ ์ ์๋ ์ ์ผ๊ฐํ์ ๋ณ์ ๊ธธ์ด์ด๋ค. P(1)๋ถํฐ P(10)๊น์ง ์ฒซ 10๊ฐ ์ซ์๋ 1, 1, 1, 2, 2, 3, 4, 5, 7, 9์ด๋ค.

N์ด ์ฃผ์ด์ก์ ๋, P(N)์ ๊ตฌํ๋ ํ๋ก๊ทธ๋จ์ ์์ฑํ์์ค.

## ์๋ ฅ

์ฒซ์งธ ์ค์ ํ์คํธ ์ผ์ด์ค์ ๊ฐ์ T๊ฐ ์ฃผ์ด์ง๋ค. ๊ฐ ํ์คํธ ์ผ์ด์ค๋ ํ ์ค๋ก ์ด๋ฃจ์ด์ ธ ์๊ณ , N์ด ์ฃผ์ด์ง๋ค. (1 โค N โค 100)

## ์ถ๋ ฅ

๊ฐ ํ์คํธ ์ผ์ด์ค๋ง๋ค P(N)์ ์ถ๋ ฅํ๋ค.

## ์์  ์๋ ฅ 1ย 

2
6
12

## ์์  ์ถ๋ ฅ 1ย 

3
16


---

### ๐ ์ ๋ต

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
  
public class Main {  
  
    public static void main(String[] args) throws IOException {  
  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        int T = Integer.parseInt(br.readLine());  
  
        StringBuilder sb = new StringBuilder();  
        long[] dp = new long[101];  
        dp[1] = 1;  
        dp[2] = 1;  
        dp[3] = 1;  
        dp[4] = 2;  
        dp[5] = 2;  
        for (int i = 6; i < 101; i++) {  
            dp[i] = dp[i-1] + dp[i-5];  
        }  
  
        for (int i = 0; i < T; i++) {  
            int n = Integer.parseInt(br.readLine());  
            sb.append(dp[n]).append("\n");  
        }  
        System.out.println(sb);  
    }  
}
```
- ๊ท์น์ ์ฐพ๋ค๊ฐ ์ฒ์์ ๋ง๋ค์ด๋ณธ ์ ํ์

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
  
public class Main {  
  
    public static void main(String[] args) throws IOException {  
  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        int T = Integer.parseInt(br.readLine());  
  
        StringBuilder sb = new StringBuilder();  
        long[] dp = new long[101];  
        dp[1] = 1;  
        dp[2] = 1;  
        dp[3] = 1;  
        for (int i = 4; i < 101; i++) {  
            dp[i] = dp[i-2] + dp[i-3];  
        }  
  
        for (int i = 0; i < T; i++) {  
            int n = Integer.parseInt(br.readLine());  
            sb.append(dp[n]).append("\n");  
        }  
        System.out.println(sb);  
    }  
}
```
- ํผ๋ณด๋์น๋ ํ์ฌ ํญ์ ๊ฐ์ ์์ ๋ ํญ์ ๊ฐ์ ํฉ์ผ๋ก ์ด๋ฃจ์ด์ง๋ค.
	- 1 1 2 3 5 8 . . .
- ๋ฌธ์ ๋ ํผ๋ณด๋์น ์์ด ํ์์ด๊ธด ํ์ง๋ง ์์ ๋ ํญ์ ํฉ์ด ํ์ฌ ํญ ๋ค์ ํญ์ ๋ํ๋๋ค.
	- 1 1 1 2 2 3 4 5 7 . . .
- ๋ฐ๋ผ์ ์ ํ์์ dp[i] = dp[i-2] + dp[i-3] ์ผ๋ก ์ธ์์ฃผ๋ฉด ๋๊ณ  dp[100]์ ๊ฒฝ์ฐ 9,000์ต ๊ฐ๊น์ด ๋๋ฏ๋ก longํ์ ๋ฐฐ์ด์ ์ ์ธํด์ ๋ด์์ฃผ์๋ค.
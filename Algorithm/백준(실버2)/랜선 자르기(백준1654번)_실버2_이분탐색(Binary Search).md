# [λ¬Έμ λ§ν¬](https://www.acmicpc.net/problem/2805)

## π λ¬Έμ 

μ§μμ μκ°μ λ³΄λ΄λ μ€μμμ λ°μ±μμ λΆλ¦μ λ°κ³  κΈν λ¬λ €μλ€. λ°μ±μμ΄Β μΊ ν λ μΈ Nκ°μ λμ μ λ§λ€μ΄μΌ νλλ° λλ¬΄ λ°λΉ μ μμμ΄μκ² λμμ μ²­νλ€.

μ΄λ―Έ μ€μμμ μμ²΄μ μΌλ‘ Kκ°μ λμ μ κ°μ§κ³  μλ€. κ·Έλ¬λ Kκ°μ λμ μ κΈΈμ΄κ° μ κ°κ°μ΄λ€. λ°μ±μμ λμ μ λͺ¨λ Nκ°μ κ°μ κΈΈμ΄μ λμ μΌλ‘ λ§λ€κ³  μΆμκΈ° λλ¬Έμ Kκ°μ λμ μ μλΌμ λ§λ€μ΄μΌ νλ€. μλ₯Ό λ€μ΄ 300cm μ§λ¦¬ λμ μμ 140cm μ§λ¦¬ λμ μ λ κ° μλΌλ΄λ©΄ 20cmλΒ λ²λ €μΌ νλ€. (μ΄λ―Έ μλ₯Έ λμ μ λΆμΌ μ μλ€.)

νΈμλ₯Ό μν΄ λμ μ μλ₯΄κ±°λ λ§λ€ λ μμ€λλ κΈΈμ΄λ μλ€κ³  κ°μ νλ©°, κΈ°μ‘΄μ Kκ°μ λμ μΌλ‘ Nκ°μ λμ μ λ§λ€ μ μλ κ²½μ°λ μλ€κ³  κ°μ νμ. κ·Έλ¦¬κ³  μλ₯Ό λλ ν­μ μΌν°λ―Έν° λ¨μλ‘ μ μκΈΈμ΄λ§νΌ μλ₯Έλ€κ³  κ°μ νμ. Nκ°λ³΄λ€ λ§μ΄ λ§λλ κ²λ Nκ°λ₯Ό λ§λλ κ²μ ν¬ν¨λλ€. μ΄λ λ§λ€ μ μλ μ΅λ λμ μ κΈΈμ΄λ₯Ό κ΅¬νλ νλ‘κ·Έλ¨μ μμ±νμμ€.

## μλ ₯

μ²«μ§Έ μ€μλ μ€μμμ΄ μ΄λ―Έ κ°μ§κ³  μλ λμ μ κ°μ K, κ·Έλ¦¬κ³  νμν λμ μ κ°μ Nμ΄ μλ ₯λλ€. Kλ 1μ΄μ 10,000μ΄νμ μ μμ΄κ³ , Nμ 1μ΄μ 1,000,000μ΄νμ μ μμ΄λ€. κ·Έλ¦¬κ³  ν­μ K β¦ N μ΄λ€. κ·Έ ν Kμ€μ κ±Έμ³ μ΄λ―Έ κ°μ§κ³  μλ κ° λμ μ κΈΈμ΄κ° μΌν°λ―Έν° λ¨μμ μ μλ‘ μλ ₯λλ€. λμ μ κΈΈμ΄λ 231-1λ³΄λ€ μκ±°λ κ°μ μμ°μμ΄λ€.

## μΆλ ₯

μ²«μ§Έ μ€μ Nκ°λ₯Ό λ§λ€ μ μλ λμ μ μ΅λ κΈΈμ΄λ₯Ό μΌν°λ―Έν° λ¨μμ μ μλ‘ μΆλ ₯νλ€.

## μμ  μλ ₯ 1Β 

4 11
802
743
457
539

## μμ  μΆλ ₯ 1

200


---

### π μ λ΅

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.*;  
  
public class Main {  
    public static void main(String[] args) throws IOException {  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        StringTokenizer st = new StringTokenizer(br.readLine());  
        int K = Integer.parseInt(st.nextToken());  
        int N = Integer.parseInt(st.nextToken());  

		// λ°°μ΄μ μλ ₯κ°μ λ΄μΌλ©΄μ λμμ maxκ° κ΅¬νκΈ°!
        int[] lines = new int[K];  
        long max = 0;  
        for (int i = 0; i < K; i++) {  
            lines[i] = Integer.parseInt(br.readLine());  
            if (max < lines[i]) max = lines[i];  
        }  
  
        long min = 0;  
        long mid = 0;  
        while (min <= max) { 
         
            mid = (min + max) / 2;  

			// μ€κ°κ°μΌλ‘ λͺ κ°μ λμ μ΄ λμ€λμ§ κ΅¬ν¨!
            long cnt = 0;  
            for (int i = 0; i < lines.length; i++) {  
                cnt += lines[i] / mid;  
            }  

			/**
			* νμν λμ  κ°μ(N)μ κ΅¬ν κ°μ(cnt)λ₯Ό λΉκ΅ν΄μ
			* λ μ λ€λ©΄ λμ μ κΈΈμ΄λ₯Ό μ€μ¬μΌ κ°μκ° λμ΄λκ³ 
			* λ λ§λ€λ©΄ λμ μ κΈΈμ΄λ₯Ό λλ €μΌ νλ€.
			*/
            if (cnt < N) max = mid - 1;  
            else min = mid + 1;  
        }
        
        System.out.println(max);  
    }  
}
```
- [μ΄λΆνμ κ°λ](/Algorithm/μ΄λΆ_νμ(Binary_Search).md)
- μ΄λΆ νμμ κΈ°λ³Έμ μΈ νμ΄λ λ°°μ΄ μμμ  `νΉμ  μΈλ±μ€` λ₯Ό μ°Ύλ κ²μ΄μλ€.
- κ·Έλ¬λ μ΄ λ¬Έμ μμλ μΈλ±μ€κ° μλλΌ `κΈΈμ΄` λ₯Ό μ°ΎμμΌ νλ―λ‘ λ²μλ `κΈΈμ΄` μ `μλ ₯κ°(lines)` μΌλ‘ λ³΄κ³  κ΅¬ν΄μΌ νλ€.
	- μ€κ°κ°(mid)μ (min+max) / 2 μΈλ°, μ΄κΈ° κ°μ min = 0 μ΄λ―λ‘ max / 2κ° μ΄κΈ° μ€κ°κ°μ΄ λλ€.
- κ·Έλ¦¬κ³  μ€κ°κ°μ κ΅¬νλ€λ©΄ νμν λμ μ κ°μ(N)κ³Ό λΉκ΅ν΄μ λ²μλ₯Ό μ’νλκ°λ€.

# [λ¬Έμ λ§ν¬](https://www.acmicpc.net/problem/1780)

## π λ¬Έμ 

NΓNν¬κΈ°μ νλ ¬λ‘ ννλλ μ’μ΄κ° μλ€. μ’μ΄μ κ° μΉΈμλ -1, 0, 1 μ€ νλκ° μ μ₯λμ΄ μλ€. μ°λ¦¬λ μ΄ νλ ¬μ λ€μκ³Ό κ°μ κ·μΉμ λ°λΌ μ μ ν ν¬κΈ°λ‘ μλ₯΄λ €κ³  νλ€.

1.  λ§μ½ μ’μ΄κ° λͺ¨λ κ°μ μλ‘ λμ΄ μλ€λ©΄ μ΄ μ’μ΄λ₯Ό κ·Έλλ‘ μ¬μ©νλ€.
2.  (1)μ΄ μλ κ²½μ°μλ μ’μ΄λ₯Ό κ°μ ν¬κΈ°μ μ’μ΄ 9κ°λ‘ μλ₯΄κ³ , κ°κ°μ μλ¦° μ’μ΄μ λν΄μ (1)μ κ³Όμ μ λ°λ³΅νλ€.

μ΄μ κ°μ΄ μ’μ΄λ₯Ό μλμ λ, -1λ‘λ§ μ±μμ§ μ’μ΄μ κ°μ, 0μΌλ‘λ§ μ±μμ§ μ’μ΄μ κ°μ, 1λ‘λ§ μ±μμ§ μ’μ΄μ κ°μλ₯Ό κ΅¬ν΄λ΄λ νλ‘κ·Έλ¨μ μμ±νμμ€.

## μλ ₯

μ²«μ§Έ μ€μ N(1 β€ N β€ 37, Nμ 3kΒ κΌ΄)μ΄ μ£Όμ΄μ§λ€. λ€μ Nκ°μ μ€μλ Nκ°μ μ μλ‘ νλ ¬μ΄ μ£Όμ΄μ§λ€.

## μΆλ ₯

μ²«μ§Έ μ€μ -1λ‘λ§ μ±μμ§ μ’μ΄μ κ°μλ₯Ό, λμ§Έ μ€μ 0μΌλ‘λ§ μ±μμ§ μ’μ΄μ κ°μλ₯Ό, μμ§Έ μ€μ 1λ‘λ§ μ±μμ§ μ’μ΄μ κ°μλ₯Ό μΆλ ₯νλ€.

## μμ  μλ ₯ 1Β 

9
0 0 0 1 1 1 -1 -1 -1
0 0 0 1 1 1 -1 -1 -1
0 0 0 1 1 1 -1 -1 -1
1 1 1 0 0 0 0 0 0
1 1 1 0 0 0 0 0 0
1 1 1 0 0 0 0 0 0
0 1 -1 0 1 -1 0 1 -1
0 -1 1 0 1 -1 0 1 -1
0 1 -1 1 0 -1 0 1 -1

## μμ  μΆλ ₯ 1Β 

10
12
11


---

### π μ λ΅

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int N;
    static int minus, zero, plus = 0;
    static int[][] papers;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        /* μλ ₯λ°κΈ° */
        papers = new int[N][N];
        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                papers[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        cutting(0, 0, N);
        System.out.println(minus + "\n" + zero + "\n" + plus);
    }

    public static void cutting(int row, int col, int size) {
        /**
         * μ²« μμλ₯Ό κΈ°μ€μΌλ‘ μ’μ΄ λ΄μ λͺ¨λ  μμκ° κ°μμ§λ₯Ό μ²΄ν¬νλ€.
         * λͺ¨λ κ°λ€λ©΄ ν΄λΉ μμ λ³μλ₯Ό μΉ΄μ΄νν΄μ€λ€!
         * κ°μ§ μλ€λ©΄ μ’μ΄λ₯Ό κ°λ‘μΈλ‘ 3λ±λΆνκ³  9κ°λ‘ λλμ΄μ§ κ΅¬μ­λ€μ κ°κ° cutting λ©μλλ‘ λΆλ₯Έλ€!
         */
        if (isSameNumber(row, col, size)) {
            if (papers[row][col] == -1) minus++;
            else if (papers[row][col] == 0) zero++;
            else plus++;

        } else {

            int cuttingSize = size / 3;

            cutting(row, col, cuttingSize);
            cutting(row, col+cuttingSize, cuttingSize);
            cutting(row, col+cuttingSize*2, cuttingSize);
            cutting(row+cuttingSize, col, cuttingSize);
            cutting(row+cuttingSize, col+cuttingSize, cuttingSize);
            cutting(row+cuttingSize, col+cuttingSize*2, cuttingSize);
            cutting(row+cuttingSize*2, col, cuttingSize);
            cutting(row+cuttingSize*2, col+cuttingSize, cuttingSize);
            cutting(row+cuttingSize*2, col+cuttingSize*2, cuttingSize);

        }
    }

    public static boolean isSameNumber(int row, int col, int size) {
        /* μ²«λ²μ§Έ μμλ₯Ό κΈ°μ€μΌλ‘ μ²΄ν¬ */
        int Num = papers[row][col];

        for (int i = row; i < row+size; i++) {
            for (int j = col; j < col+size; j++) {
                if (papers[i][j] != Num) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
- λ©°μΉ  μ μ νμλ μμ’μ΄ λ¬Έμ μ κ±°μ λΉμ·ν λ¬Έμ μλ€! κ·Έ λλ λ΅μ λ³΄κ³  μ΄ν΄ν νμ μ½λννλ©΄μλ κ³μ λ΅μμ μ°Έκ³ νλ©΄μ μμ±νμμλλ° μ΄λ²μλ νΌμ νμΌλ‘ νμ΄λ΄μ λ§€μ° λΏλ―νλ€!

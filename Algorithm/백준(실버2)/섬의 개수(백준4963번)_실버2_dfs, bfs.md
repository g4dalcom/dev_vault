# [λ¬Έμ λ§ν¬](https://www.acmicpc.net/problem/4963)

## π λ¬Έμ 

μ μ¬κ°νμΌλ‘ μ΄λ£¨μ΄μ Έ μλ μ¬κ³Ό λ°λ€ μ§λκ° μ£Όμ΄μ§λ€. μ¬μ κ°μλ₯Ό μΈλ νλ‘κ·Έλ¨μ μμ±νμμ€.

![](https://www.acmicpc.net/upload/images/island.png)

ν μ μ¬κ°νκ³Ό κ°λ‘, μΈλ‘ λλ λκ°μ μΌλ‘ μ°κ²°λμ΄ μλ μ¬κ°νμ κ±Έμ΄κ° μ μλ μ¬κ°νμ΄λ€.Β 

λ μ μ¬κ°νμ΄ κ°μ μ¬μ μμΌλ €λ©΄, ν μ μ¬κ°νμμ λ€λ₯Έ μ μ¬κ°νμΌλ‘ κ±Έμ΄μ κ° μ μλ κ²½λ‘κ° μμ΄μΌ νλ€. μ§λλ λ°λ€λ‘ λλ¬μΈμ¬ μμΌλ©°, μ§λ λ°μΌλ‘ λκ° μ μλ€.

## μλ ₯

μλ ₯μ μ¬λ¬ κ°μ νμ€νΈ μΌμ΄μ€λ‘ μ΄λ£¨μ΄μ Έ μλ€. κ° νμ€νΈ μΌμ΄μ€μ μ²«μ§Έ μ€μλ μ§λμ λλΉ wμ λμ΄ hκ° μ£Όμ΄μ§λ€. wμ hλ 50λ³΄λ€ μκ±°λ κ°μ μμ μ μμ΄λ€.

λμ§Έ μ€λΆν° hκ° μ€μλ μ§λκ° μ£Όμ΄μ§λ€. 1μ λ, 0μ λ°λ€μ΄λ€.

μλ ₯μ λ§μ§λ§ μ€μλ 0μ΄ λ κ° μ£Όμ΄μ§λ€.

## μΆλ ₯

κ° νμ€νΈ μΌμ΄μ€μ λν΄μ, μ¬μ κ°μλ₯Ό μΆλ ₯νλ€.

## μμ  μλ ₯ 1Β 

1 1
0
2 2
0 1
1 0
3 2
1 1 1
1 1 1
5 4
1 0 1 0 0
1 0 0 0 0
1 0 1 0 1
1 0 0 1 0
5 4
1 1 1 0 1
1 0 1 0 1
1 0 1 0 1
1 0 1 1 1
5 5
1 0 1 0 1
0 0 0 0 0
1 0 1 0 1
0 0 0 0 0
1 0 1 0 1
0 0

## μμ  μΆλ ₯ 1Β 

0
1
1
3
1
9


---

### π μ λ΅

### DFS

```java
import java.io.BufferedReader;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.util.*;  
  
public class Main {  
    static int w, h;  
    static int[][] islands;  
    static boolean[][] visit;  
  
    public static void main(String[] args) throws IOException {  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        StringBuilder sb = new StringBuilder();  
  
        while (true) {  
            StringTokenizer st = new StringTokenizer(br.readLine());  
            w = Integer.parseInt(st.nextToken()); // μ§λμ λλΉ  
            h = Integer.parseInt(st.nextToken()); // μ§λμ λμ΄  
  
            /* μλ ₯κ°μ΄ 0 0 μ΄λ©΄ μλ ₯ μ’λ£! */  
            if (w == 0 && h == 0) break;  
  
            /* μ¬μ μ’νλ₯Ό μλ ₯λ°μ λ°°μ΄ */            islands = new int[h][w];  
            visit = new boolean[h][w];  
  
            /* μλ ₯ λ°κΈ° */            for (int i = 0; i < h; i++) {  
                st = new StringTokenizer(br.readLine());  
                for (int j = 0; j < w; j++) {  
                    islands[i][j] = Integer.parseInt(st.nextToken());  
                }  
            }  
  
            /**  
             * [0, 0] λΆν° μμν΄μ μ¬μ΄λ©΄μ λ°©λ¬Ένμ§ μμλ λΈλλΌλ©΄ dfs ν¨μλ₯Ό νκ³ ,  
             * dfs ν¨μμμ μ΄μ΄μ§ λͺ¨λ  κ³³μ νμν ν λμ€λ©΄ μΉ΄μ΄νμ νλ€  
             * dfs ν¨μ λ΄μμ μ΄μ΄μ§ κ³³λ€μ νμνλ©΄μ visit = trueλ₯Ό ν΄μ£ΌκΈ° λλ¬Έμ  
             * λ€μ dfsν¨μλ₯Ό ν λλ μ΄μ μ νμν κ³³κ³Ό μ΄μ΄μ§μ§ μμ κ³³λΆν° λ€μ νμνκ² λ  κ²μ΄λ€!  
             */            int cnt = 0;  
            for (int i = 0; i < h; i++) {  
                for (int j = 0; j < w; j++) {  
                    if (islands[i][j] == 1 && !visit[i][j]) {  
                        cnt++;  
                        dfs(i, j);  
                    }  
                }  
            }  
            sb.append(cnt).append("\n");  
        }  
        System.out.println(sb);  
    }  
  
    public static void dfs(int x, int y) {  
        /* μ£Όλ³μ μ΄μ΄μ§ κ³³μ νμνκΈ° μν μ’ν */        int[] cx = {0, 0, -1, 1, 1, 1, -1, -1};  
        int[] cy = {1, -1, 0, 0, 1, -1, -1, 1};  
  
        visit[x][y] = true;  
  
        /* ν΄λΉ μ’νμμ μνμ’μ°λκ°μ κΉμ§ μ΄μ΄μ§ κ³³μ νμνκΈ° μν΄ μ’νλ₯Ό λλ λ‘μ§ */        for (int i = 0; i < cx.length; i++) {  
            int dx = x + cx[i];  
            int dy = y + cy[i];  
  
            /* νμνλ κ³³μ΄ μ§λ μμͺ½μ΄λ©΄μ, μ¬μ΄κ³ , λ°©λ¬Ένμ§ μμλ€λ©΄ κ·Έ μ’νλ‘ dfs μ¬κ· νΈμΆ! */  
            if (dx >= 0 && dy >= 0 && dx < h && dy < w) {  
                if (islands[dx][dy] == 1 && !visit[dx][dy]) {  
                    dfs(dx, dy);  
                }  
            }  
        }  
    }  
}
```

### BFS

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int w, h;
    static int[][] islands;
    static boolean[][] visit;
    static int[] cx = {0, 0, -1, 1, 1, 1, -1, -1};
    static int[] cy = {1, -1, 0, 0, 1, -1, -1, 1};
    static class Node {
        int x, y;
        public Node(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        while (true) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            w = Integer.parseInt(st.nextToken()); // μ§λμ λλΉ
            h = Integer.parseInt(st.nextToken()); // μ§λμ λμ΄

            /* μλ ₯κ°μ΄ 0 0 μ΄λ©΄ μλ ₯ μ’λ£! */
            if (w == 0 && h == 0) break;

            /* μ¬μ μ’νλ₯Ό μλ ₯λ°μ λ°°μ΄ */
            islands = new int[h][w];
            visit = new boolean[h][w];

            /* μλ ₯ λ°κΈ° */
            for (int i = 0; i < h; i++) {
                st = new StringTokenizer(br.readLine());
                for (int j = 0; j < w; j++) {
                    islands[i][j] = Integer.parseInt(st.nextToken());
                }
            }

            /**
             * [0, 0] λΆν° μμν΄μ μ¬μ΄λ©΄μ λ°©λ¬Ένμ§ μμλ λΈλλΌλ©΄ dfs ν¨μλ₯Ό νκ³ ,
             * bfs ν¨μμμ μ΄μ΄μ§ λͺ¨λ  κ³³μ νμν ν λμ€λ©΄ μΉ΄μ΄νμ νλ€
             * bfs ν¨μ λ΄μμ μ΄μ΄μ§ κ³³λ€μ νμνλ©΄μ visit = trueλ₯Ό ν΄μ£ΌκΈ° λλ¬Έμ
             * λ€μ bfsν¨μλ₯Ό ν λλ μ΄μ μ νμν κ³³κ³Ό μ΄μ΄μ§μ§ μμ κ³³λΆν° λ€μ νμνκ² λ  κ²μ΄λ€!
             */
            int cnt = 0;
            for (int i = 0; i < h; i++) {
                for (int j = 0; j < w; j++) {
                    if (islands[i][j] == 1 && !visit[i][j]) {
                        cnt++;
                        bfs(i, j);
                    }
                }
            }
            sb.append(cnt).append("\n");
        }
        System.out.println(sb);
    }

    public static void bfs(int x, int y) {
	    /* ν μ μΈνκ³  μ΄κΈ°κ° λ£μ΄μ£ΌκΈ° */
        Queue<Node> q = new LinkedList<>();
        q.offer(new Node(x, y));

        visit[x][y] = true;

        while (!q.isEmpty()) {
			/* νμ μλ κ²μ μμ°¨μ μΌλ‘ λΉΌμ€λ€! */
            Node node = q.poll();

			/* μνμ’μ°λκ°μ κΉμ§ μ΄μ΄μ§ κ³³ νμ */
            for (int i = 0; i < cx.length; i++) {
                int dx = node.x + cx[i];
                int dy = node.y + cy[i];

				/**
				* dfsμ²λΌ μ€κ°μ μ¬κ·νΈμΆμ νμ§ μκ³  μ£Όλ³ λͺ¨λ  κ³³μ νμνλ©΄μ
				* μ§λ λ²μ λ΄μ μκ³ , μ¬μ΄κ³ , λ°©λ¬Ένμ§ μμ κ³³μ΄λΌλ©΄ νμ μ°¨λ‘λλ‘ λ£μ΄μ€λ€!
				* νκ° λΉ λκΉμ§ μ£Όλ³μ μ£Όλ³μ μ£Όλ³μ λλ©΄μ μ΄μ΄μ§ κ³³λ€μ λͺ¨λ λ°κ²¬ν  κ²μ΄λ€!
				*/
                if (dx >= 0 && dy >= 0 && dx < h && dy < w) {
                    if (islands[dx][dy] == 1 && !visit[dx][dy]) {
                        visit[dx][dy] = true;
                        q.offer(new Node(dx, dy));
                    }
                }
            }
        }
    }
}
```
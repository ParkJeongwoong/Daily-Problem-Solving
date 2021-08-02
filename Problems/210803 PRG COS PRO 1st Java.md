# 210803 PRG COS PRO 1st Java

링크 : https://programmers.co.kr/learn/courses/11132/lessons/71155

제목 : 프로그래머스 COS Pro 1급 Java 꽃피우기

유형 : BFS

---

```java
// 다음과 같이 import를 사용할 수 있습니다.
import java.util.*;
import java.util.Queue;
import java.util.LinkedList;

class Solution {
    public int solution(int[][] garden) {
        // 여기에 코드를 작성해주세요.
        Queue <Node> queue = new LinkedList<>();
        for (int i=0;i<garden.length;i++) {
            for (int j=0;j<garden[i].length;j++) {
                if (garden[i][j] == 1) {
                    queue.add(new Node(i,j));
                }
            }
        }
        
        int day = 0;       
        
        while (!queue.isEmpty()) {
            int todaysFlower = queue.size();
            boolean flag = false;
            
            for (int i=0;i<todaysFlower;i++){
                Node flower = queue.poll();
                // 좌
                if (flower.x>0 && garden[flower.x-1][flower.y] == 0) {
                    flag = true;
                    garden[flower.x-1][flower.y] = 1;
                    queue.add(new Node(flower.x-1, flower.y));
                };
                // 우
                if (flower.x<garden.length-1 && garden[flower.x+1][flower.y] == 0) {
                    flag = true;
                    garden[flower.x+1][flower.y] = 1;
                    queue.add(new Node(flower.x+1, flower.y));
                };
                // 상
                if (flower.y>0 && garden[flower.x][flower.y-1] == 0) {
                    flag = true;
                    garden[flower.x][flower.y-1] = 1;
                    queue.add(new Node(flower.x, flower.y-1));
                };
                // 하
                if (flower.y<garden[0].length-1 && garden[flower.x][flower.y+1] == 0) {
                    flag = true;
                    garden[flower.x][flower.y+1] = 1;
                    queue.add(new Node(flower.x, flower.y+1));
                };
            }
            
            if (flag) {
                day += 1;      
            };
        };
        
        return day;
    }
    
    class Node{
    int x;
    int y;

    Node(int _x, int _y){
        this.x = _x;
        this.y = _y;
        }
    }
    
    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[][] garden1 = {{0, 0, 0}, {0, 1, 0}, {0, 0, 0}};
        int ret1 = sol.solution(garden1);
        
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret1 + " 입니다.");
        
        int[][] garden2 = {{1, 1}, {1, 1}};
        int ret2 = sol.solution(garden2);
        
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret2 + " 입니다.");
        
    }    
}
```


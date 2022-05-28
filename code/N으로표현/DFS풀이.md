
```java
public class Solution {

static int min = Integer.MAX_VALUE; // 최솟값 하나 셋팅 
    
    public static int solution(int N, int number) {
        
    	dfs(0, N, number, 0);
        
        if (min == Integer.MAX_VALUE) return -1;
        return min;
    }
    
    public static void dfs(int depth, int N, int number, int current) {
        if (depth > 8) {
            return;
        }
        
        if (number == current) { // 찾고자 하는 값이 만들어지면 ,최소값을 찾아서 리턴하고 스탑 한다. 
            min = Math.min(depth, min);
            return;
        }
        
        int temp = 0;  // 새로운 dfs 호출시 마다 0으로 초기화 
            
        for (int i = 0; i < 8; i++) { //  8 넘어가면 -1 리턴 하라고 했으므로 
            if (depth + i < 8) {
                temp = temp * 10 + N;
                /* 새로운 dfs 호출시 마다 
                 * 5 , 55, 555, 5555 를 만들어 준다.
                 */
                dfs(depth + i + 1, N, number, current + temp);
                dfs(depth + i + 1, N, number, current - temp);
                dfs(depth + i + 1, N, number, current / temp);
                dfs(depth + i + 1, N, number, current * temp);     
            }      
        }
    }
    
	public static void main(String[] args) {
		System.out.println(solution(5,12));
		
	}

}
```

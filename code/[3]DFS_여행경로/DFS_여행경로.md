```java
import java.util.*;
class Solution {
	boolean [] used;
	ArrayList<String> list ;

	public String[] solution(String[][] tickets) {
        list = new ArrayList<String>();
        used = new boolean[tickets.length];
        dfs(tickets, 0, used, "ICN","ICN");
        
        Collections.sort(list);
        
        return list.get(0).split(" ");
    }
	
	public void dfs(String [][]tickets, int depth, boolean [] used, String nowVal, String path) {
		
		if(depth==tickets.length) { // 한바퀴 다 돌면 종료 
			list.add(path);			
			return;
		}
		
		for(int i = 0; i<tickets.length; i++) {
			if(used[i]) {
				continue;
			}
			
			if(!used[i] && nowVal.equals(tickets[i][0])) {
				used[i] = true;
				dfs(tickets, depth+1, used,tickets[i][1], path +" "+tickets[i][1]); // path에는 정답 경로를 기록해둔다. 
				used[i] = false; // 모든 경로를 다 탐색해봐야 하기 때문에 풀어준다. 
			}
		}
	}
    
}
```

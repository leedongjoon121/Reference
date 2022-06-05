
```java
public class Solution {

static int min = Integer.MAX_VALUE; // 최솟값 하나 셋팅 
    
    public static int solution(int N, int [][] computers) {
      int answer = 0;
      boolean [] visited = new boolean[computers.length];
      
      for(int i = 0; i< computers.length; i++) {
    	  visited[i] = false; // 처음에는 다 방문안한거로 초기화 
      }
      
      for(int i = 0; i<computers.length; i++) {
    	  
    	  if(visited[i]==false) { // 방문을 안했다고 가정할 경우에만 DFS 시작 
    		  answer++; // 만약 모든 노드가 다 이어져 있어도 1개 이다. 그러므로 최소 정답이 1 
    		  dfs(i, visited,computers);
    	  }
      }
    	
      return answer;
    }
    
    
    // 한 노드로 부터 쭉~ 연결된 모든걸 다 이어버림 ,  그래서 다 이어진 거는 1개로 침 
    public static void dfs(int node, boolean[] visited, int[][]computers) {
    	visited[node] = true;
    	
    	for(int i = 0; i<computers.length; i++) {
    		                         // 1로 표기됐으면 전부다 이어버림, 이어지면 1개로 치는거임 
    		if(visited[i]==false && computers[node][i] == 1) {
    			dfs(i, visited, computers);
    		}
    		
    	}
    }
    
	public static void main(String[] args) {
		int [][]computers = { {1, 1, 0}, {1, 1, 0}, {0, 0, 1} };
		System.out.println("정답 : "+solution(3,computers));

	}

}
```

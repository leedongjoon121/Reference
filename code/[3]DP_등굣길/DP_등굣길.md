```java
class Solution {
    public int solution(int m, int n, int[][] puddles) {
        
        int board[][] = new int [n+1][m+1];
		int mod = 1000000007;
		board[1][1] = 1;
		
        // 첫 번째 가로 , 세로 줄은 전부 1로 초기화 
		for(int i = 1; i <= m; i++) {
			board[1][i] = 1;
		}
		
		for(int i = 1; i <= n; i++) {
			board[i][1] = 1;
		}
		
        // 웅덩이 셋팅 
		for( int i = 0; i < puddles.length; i ++ ) {
			// 문제에서 m,n이 세로 가로 이므로 ...   x,y를 거꾸로 놓는다... 문제 이상함 
            int x = puddles[i][1];
			int y = puddles[i][0];
			
			board[x][y] = -1;
		}
		
		for(int i = 1; i <= n; i++) {
			for(int j = 1; j <= m ; j++) {
				
				if(board[i][j] == -1) { // 웅덩이 셋팅 
					board[i][j] = 0;
				}else {
					if( !(i == 1 && j == 1) ) { // 시작점은 제외 
						
						int left = board[i-1][j]; // 위쪽 
						int top = board[i][j-1]; // 왼쪽 
						
						board[i][j] = (left + top) % mod ; // 더해주기 
						
				
					}
				}
				
			}
		}
		return board[n][m];
    }
}
```

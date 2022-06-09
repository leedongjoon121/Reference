```java
import java.util.*;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int [commands.length];
        int rows = commands.length;
        for(int p = 0 ; p < rows; p++){
            int i = commands[p][0];
            int j = commands[p][1];
            int k = commands[p][2];
            
            answer[p] = solve(i,j,k,array);
        }
        return answer;
    }
    
    public int solve (int i , int j , int k, int [] array){
        int [] newArr = new int [j-i+1];
        int index = 0;
        for(int p = i-1; p < j; p++ ){            
            newArr[index] = array[p];
            index++;
        }
        Arrays.sort(newArr);
        
        return newArr[k-1];
    }
}
```

## 풀이

```java

import java.util.Arrays;
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for(int i=0; i<commands.length; i++){
            int[] temp = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(temp);
            answer[i] = temp[commands[i][2]-1];
        }

        return answer;
    }
}
```

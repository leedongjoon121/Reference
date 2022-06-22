## 기본 로직

## BFS
```java
	public static boolean [] visitied = new boolean[9];
	public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();)

	public static void bfs(int start) {
		Queue<Integer> queue = new LinkedList<>();
		queue.offer(start); 
		visitied[start] = true; // 현재 노드 방문 처리 
		
		while(!queue.isEmpty()) {
			int x = queue.poll();
			System.out.println(x+ " ");
			
			for(int i = 0; i < graph.get(x).size(); i++) {
				int v = graph.get(x).get(i);
				if(!visitied[v]) {
					queue.offer(v); // 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽
					visitied[v] = true;
				}
			}
			
		}
	}
```

<br/>

## DFS

```java
	public static boolean [] visitied = new boolean[9];
	public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();)

	public static void dfs(int x) {
		visitied[x] = true;
		System.out.println(x + " ");
		
		for(int i = 0; i < graph.get(x).size(); i++) {
			int v = graph.get(x).get(i);
			if(!visitied[v]) dfs(v);
		}
	}
```

# 입출력

# 입력
## Scanner와 BufferedReader 차이

### Scanner는 공백과 개행문자를 경계로 입력 값을 인식하기 때문에 사용이 매우 편리하지만 느리다는 단점 

```swift
  Scanner sc = new Scanner(System.in);
  int num = sc.nextInt();
  sc.close();
```

### BufferedReader는 개행 문자까지 인식하고 입력받은 값을 String 형식의 리턴값으로 반환한다.
- 때문에 필요한 데이터를 가공하는 과정이 필요하며, 번거롭지만 속도가 빠르다.
- 반드시 try & catch나 throws를 통해 예외처리를 해주어야 한다.


### BufferdReader를 사용하면서 데이터를 가공하는 방법으로는 StringTokenizer를 이용하거나, split()함수를 이용하는 방법이 있다.

#### StringTokenizer 이용시
```swift
  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
  StringTokenizer st = new StringTokenizer(br.readLine()); // 값을 한줄씩(개행 단위) 입력 받음
  
  // st에는 한줄 단위로 값을 담고 있다.
  
  // nextToken()을 이용하여 데이터를 공백 기준으로 자르고 String으로 리턴한다.
  int num1 = Integer.ParseInt(st.nextToken()); // 공백으로 짜름 , 숫자가 필요하므로 변환
  int num2 = Integer.ParseInt(st.nextToken()); // 공백으로 짜름
  br.close(); 
  
  // 1. 이와같이 사용하면, 입력 받은 한 줄에서 공백을 기준으로 구분하여 문자열 단위를 반환해준다.
  // 2. 이 반환받은 문자열을 필요에 맞게 가공하여 사용하면 된다.
  
  
  // 3. StringTokenizer는 두번째 인자에 별도로 구분자를 추가할 수도 있다.
  String str = "this%%is%%my%%string";
  StringTokenizer st = new StringTokenizer(str,"%%");
  
  while(st.hasMoreTokens()){
    System.out.println(st.nextToken());
  }
  
```

#### split 이용시
```swift
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String [] s = br.readLine().split(" ");  // 공백 단위로 값을 입력 받겠다.
         //  1 2 3 4 5 6    -> 이런식으로 입력 받을 수 있음 
```


#### 예시 2

```swift
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main  {
 
	static int N, M, K;
	static int[][] map;

	public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		StringTokenizer st = new StringTokenizer(br.readLine());// 첫 줄
		N = Integer.parseInt(st.nextToken());// 클래스 객체에서 다음 토큰을 읽음

		st = new StringTokenizer(br.readLine());// 두 번째 줄
		M = Integer.parseInt(st.nextToken());
		K = Integer.parseInt(st.nextToken());
		System.out.println(N);
		System.out.println(M + " " + K);

		map = new int[K + 1][M + 1];

		for (int i = 1; i <= K; i++) {
			st = new StringTokenizer(br.readLine());// 세번째 줄 부터 K번째 줄 까지
			for (int j = 1; j <= M; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());
				System.out.print(map[i][j] + " ");
			}
			System.out.println();
		}

}
}

```


<hr/>

# 출력

## BufferedWriter
일반적으로 편리하게 System.out.println() 함수를 출력함수로 사용하지만, 많은 양의 출력이 필요할 때는 BufferedWriter를 이용해주는 것이 좋다.

```swift
  BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
  bw.write("Hello"); // 버퍼에 출력할거 저장 
  bw.flush(); // 버퍼에 저장해 놓은거 출력
  bw.close();
```
BufferedWriter는 write()함수를 이용해서 출력 값들을 버퍼에 저장해 두고, flush()함수를 호출하여 출력한다.
BufferedWriter 같은 경우는 System.out.println()과 다르게, 자동으로 줄바꿈을 해주지 않으므로 '\n'을 통해 줄바꿈을 해주어야 한다.

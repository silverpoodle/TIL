### Scanner

`java.util 패키지의 클래스, 공백(띄어쓰기) 또는 개행(줄 바꿈)을 기준으로 읽는다.`
`Scanner는 지원해주는 메소드가 많고 사용하기 쉽기 때문에 많이 사용하지만, 버퍼 사이즈가 1024 char이기 때문에많은 입력을 필요로 할 경우에는 성능상 좋지 못한 결과를 불러온다. `

```java
Scanner in = new Scanner(System.in); // Scanner 객체 생성

in.nextByte()		// byte 형 입력 및 리턴
in.nextShort()		// short 형 입력 및 리턴
in.nextInt()		// int 형 입력 및 리턴
in.nextLong()		// long 형 입력 및 리턴
 
in.nextFloat()		// float 형 입력 및 리턴
in.nextDouble()		// double 형 입력 및 리턴
 
in.nextBoolean()	// boolean 형 입력 및 리턴
 
in.next()			// String 형 입력 및 리턴	(공백을 기준으로 한 단어를 읽음)
in.nextLine()		// String 형 입력 및 리턴 (개행을 기준으로 한 줄을 읽음)

```





### BufferedReader

`java.io 패키지의 클래스로, 개행문자만 경계로 인식하고 입력받은 데이터가 String으로 고정된다. `
`때문에 따로 데이터를 가공해야하는 경우가 많다. 하지만 Scanner보다 속도가 빠르고, 8192 char(16,384byte) 이기 때문에 입력이 많을 때 BufferedReader가 유리하다`
`또한 BufferedReader는 동기화 되기 때문에 멀티 쓰레드 환경에서 안전하다 (Scanner는 동기화가 되지 않음)`

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); // BufferedReader 객체 생성

String s = br.readLine(); // 입력(String 고정

int i = Integer.parseInt(br.readLine()); // 다른 타입으로 입력 받을 시 형변환 필수

/* 공백 단위로데이터 가공 시 */
//1. StringTokenizer 사용
StringTokenizer st = new StringTokenizer(s); //StringTokenizer인자값에 입력 문자열 넣음
int a = Integer.parseInt(st.nextToken()); //첫번째 호출
int b = Integer.parseInt(st.nextToken()); //두번째 호출
st.hasMoreTokens() //개행 전까지

//2.String.split(" ") 사용
String array[] = s.split(" "); //공백마다 데이터 끊어서 배열에 넣음
```





### BufferedWriter

`System.out.println은 적은 양일 때 사용. 많은 양의 출력을 할 때는, 입력과 동일하게 버퍼를 사용하는 것이 좋다.`

```java
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out)); // BufferedWriter 객체 생성
String str = "abcdef"; // 출력할 문자열

bw.write(s); // 출력
bw.newLine(); // 줄바꿈
bw.flush(); // 남아있는 데이터 모두 출력(스트림 비움)
bw.close() //스트림 닫음
  
// BufferedWriter의 경우 버퍼를 잡아 놓았기 때문에 반드시 사용한 후에, flush()/ close()를 해주어야 한다. 
// close()를 하게되면, 출력 스트림을 아예 닫아버리기 때문에 한번 출력후, 다른 것도 출력하고자 한다면 flush()를 사용하면 된다.
```





### StringBuilder

`동기화를 지원하지 않아 멀티 쓰레드 환경에 사용하기 적합하지 않다. `
`대신, 동기화를 지원하지 않기에 단일쓰레드에서는 StringBuffer보다 성능이 뛰어나다.`

`즉, 문자열의 연산이 자주 일어나는 단일 쓰레드 환경에서 사용하는 것이 유리하다.`



```java
StringBuilder sb = new StringBuilder();

sb.append("a");
sb.append("b").append(" ");
sb.append("c").append("\n"); // StringBuilder 뒤에 값을 붙임

sb.delete(int start , int end)  // 특정 인덱스부터 인덱스까지를 삭제
  
sb.insert(int offet, any primitive of a char[]) // 문자를 삽입함
  
sb.replace(int start , int end , String s) // 일부를 String 객체로 치환
  
sb.reverse() // 순서를 뒤집음
  
sb.setCharAt(int index , char ch) // 주어진 문자를 치환
  
sb.indexOf(String s) // 값이 어느 인덱스에 들어있는지 확인
  
sb.subString(int start, int end) // start와 end 사이의 값을 잘라옴.
```







#### 참고

String은 불변 속성을 갖고, StringBuffer/StringBuilder는 그렇지 않다.

**불변성:**
concat이나 +  연산을 통해 값을 변경하게 되면 원래 기존의 String 메모리에서 값이 바뀌는 것이 아니라
기존의 String에 들어있던 값을 버리고 새로운 값을 재할당하게 된다.
처음에 할당한 String의 메모리 영역은 Garbage로 남아있다가 GarbageCollection에 의해 없어진다.

**가변성:**
.append() , .delete()등 동일 객체 내에서 문자열을 변경하는 것이 가능하다. 
그렇게 때문에 문자열의 추가, 수정, 삭제가 빈번하게 발생할 경우 더욱 유리하다.

String은 불변성을 가지기 때문에 변하지 않는 문자열을 자주 읽어들이는 경우 사용하면 유리하다. 
하지만 문자열 추가, 삭제, 수정 등의 연산이 자주 일어나는 경우에 String을 사용하면, 힙 메모리에 많은 Garbage가 생성되고, 이는 힙 메모리 부족으로 이어져 프로그램의 성능에 치명적 영향을 미칠 수 있다.

<img src="https://blog.kakaocdn.net/dn/cog8fW/btq0c2EzgQF/Hmr8Fz7qEY0XkXOs0VNQsk/img.png" alt="img" style="zoom:60%;" />
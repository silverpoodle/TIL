컴퓨터의 IP 주소는 매번 재부팅 될 때마다 변경되는데, 이는 **DHCP(Dynamic Host Configuration Protocol)** 라는 프로토콜 때문입니다. DHCP는 네트워크에 연결된 기기들에게 자동으로 IP 주소를 할당하는 역할을 하는데, 이 방식이 사용되면 네트워크 관리가 편리해지지만 재부팅 등의 이유로 기기가 네트워크와 잠시 연결이 끊겼다가 다시 연결될 때 새로운 IP 주소를 받게 됩니다.

참고: https://learn.microsoft.com/ko-kr/windows-server/networking/technologies/dhcp/dhcp-top

<br>

IP 주소가 변경되면 서버와의 연결이 끊기는 문제가 발생할 수 있습니다. 특히, 서버가 클라이언트를 IP 주소를 통해 식별하는 경우, IP 주소가 바뀌면 서버는 그 클라이언트를 새로운 기기로 인식하게 됩니다. 

-> 고정 IP를 사용하여 이러한 문제를 해결습니다



참고한 블로그 공유해드립니다!

https://lkoon.tistory.com/entry/%EC%9C%88%EB%8F%84%EC%9A%B011-%EA%B3%A0%EC%A0%95IP-%EC%84%A4%EC%A0%95





java.lang.IllegalArgumentException: When allowCredentials is true, allowedOrigins cannot contain the special value "*" since that cannot be set on the "Access-Control-Allow-Origin" response header. To allow credentials to a set of origins, list them explicitly or consider using "allowedOriginPatterns" instead



```java
config.setAllowCredentials(*true*);
config.addAllowedOriginPattern("*");
config.addAllowedHeader("*");
config.addAllowedMethod("*");
```



![image-20231108202558014](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20231108202558014.png)

```css
/* 관리자 웹 페이지 - 로그인 */

position: relative;
width: 1920px;
height: 1080px;

background: #FFFFFF;


/* Rectangle 78 */

position: absolute;
width: 802px;
height: 1080px;
left: 0px;
top: 0px;

background: #443D3D;


/* 관리자 페이지 */

position: absolute;
width: 185px;
height: 36px;
left: 309px;
top: 696px;

font-family: 'Inter';
font-style: normal;
font-weight: 700;
font-size: 32px;
line-height: 114.02%;
/* or 36px */

color: #FFFFFF;



/* mainlogo 1 */

position: absolute;
width: 300px;
height: 303.45px;
left: 251px;
top: 364px;

background: url(mainlogo.png);


/* 비밀번호 */

position: absolute;
width: 778px;
height: 86px;
left: 953px;
top: 364px;



/* 비밀번호 */

position: absolute;
width: 733px;
height: 86px;
left: 998px;
top: 364px;

background: #DAD8D8;
border-radius: 10px;


/* 아이디 */

position: absolute;
width: 203px;
height: 29px;
left: 953px;
top: 396px;

font-family: 'Inter';
font-style: normal;
font-weight: 500;
font-size: 24px;
line-height: 114.02%;
/* or 27px */
text-align: center;

color: #6D6C6C;



/* 아이디 */

position: absolute;
width: 747px;
height: 86px;
left: 984px;
top: 504px;



/* 아이디 */

position: absolute;
width: 733px;
height: 86px;
left: 998px;
top: 504px;

background: #DAD8D8;
border-radius: 10px;


/* 비밀번호 */

position: absolute;
width: 172px;
height: 29px;
left: 984px;
top: 537px;

font-family: 'Inter';
font-style: normal;
font-weight: 500;
font-size: 24px;
line-height: 114.02%;
/* or 27px */
text-align: center;

color: #6D6C6C;



/* 버튼 */

position: absolute;
width: 733px;
height: 86px;
left: 998px;
top: 696px;



/* 버튼 */

position: absolute;
width: 733px;
height: 86px;
left: 998px;
top: 696px;

background: #443D3D;
border-radius: 10px;


/* 로그인 */

position: absolute;
width: 172px;
height: 49px;
left: 1278px;
top: 715px;

font-family: 'Inter';
font-style: normal;
font-weight: 800;
font-size: 40px;
line-height: 114.02%;
/* or 46px */
text-align: center;

color: #FFFFFF;


```



```java
  Mono<String> firstResponse = Mono.just("일 ");
//        Mono<String> secondResponse = Mono.just("이 ");
//        Mono<String> thirdResponse = Mono.just("쓰리 ");
//        Mono<String> fourthResponse = Mono.just("사 ");
//        Mono<String> fifthResponse = Mono.just("오 ");
//
//        Flux<ServerSentEvent<String>> responseStream = Flux.concat(
//                firstResponse.map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                secondResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                thirdResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                fourthResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                fifthResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                secondResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                thirdResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                fourthResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build()),
//                fifthResponse.delayElement(Duration.ofSeconds(1)).map(data -> ServerSentEvent.<String>builder().data(data).build())
//        );

//        return responseStream;
```





```
Error: Cannot find module 'typescript' from 'C:\Users\user\Desktop\runninghi\runninghi-front\node_modules'
    at Function.resolveSync [as sync] (C:\Users\user\AppData\Roaming\npm\node_modules\react-scripts\node_modules\resolve\lib\sync.js:111:15)
    at getModules (C:\Users\user\AppData\Roaming\npm\node_modules\react-scripts\config\modules.js:119:32)
    at Object.<anonymous> (C:\Users\user\AppData\Roaming\npm\node_modules\react-scripts\config\modules.js:142:18)
    at Module._compile (node:internal/modules/cjs/loader:1256:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1310:10)
    at Module.load (node:internal/modules/cjs/loader:1119:32)
    at Module._load (node:internal/modules/cjs/loader:960:12)
    at Module.require (node:internal/modules/cjs/loader:1143:19)
    at require (node:internal/modules/cjs/helpers:121:18)
    at Object.<anonymous> (C:\Users\user\AppData\Roaming\npm\node_modules\react-scripts\config\webpack.config.js:28:17) {
  code: 'MODULE_NOT_FOUND'
}
```

```
npm install typescript
```


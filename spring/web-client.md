## BodyInserter 와 bodyValue 의 차이



### BodyInserter

```java
webClient.post()
    .uri("/resource")
    .body(BodyInserters.fromValue(requestBody))
    .retrieve()
    .bodyToMono(Response.class);
```

- 더욱 세밀한 제어를 위해 사용
- request 의 insert 방법을 자체적으로 정의 가능



### bodyValue

```java
webClient.post()
    .uri("/resource")
    .bodyValue(requestBody)
    .retrieve()
    .bodyToMono(Response.class);

```

- 간단한 요청을 보낼 때
- 별다른 처리 없이 간단한 객체를 request body 로 전송 할 때








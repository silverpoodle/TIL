#### Authorization(인증)

` 해당 사용자가 본인이 맞는지를 확인하는 절차`

#### Authentication(인가)

`인증된 사용자가 해당 자원에 접근 가능한지를 결정하는 절차`



#### Authorization Architecture



![보안컨텍스트홀더](https://docs.spring.io/spring-security/reference/_images/servlet/authentication/architecture/securitycontextholder.png)

- SecurityContextHolder
  - Principal : 사용자 식별 (접근 주체) -> 보통 UserDetails의 instance
  - Credentials : 비밀번호 (인증 후 삭제)
  - Authorities : roles(역할), scope(범위) 
  - SecurityContext : 현재 인증된 사용자의 세부 정보를 저장





![providermanagers parent](https://docs.spring.io/spring-security/reference/_images/servlet/authentication/architecture/providermanagers-parent.png)

- AuthenticationManager : Spring Security의 필터가 인증을 수행하는 방법을 정의하는 API

  ​						-> 컨트롤러에 의해 호출되어 반환된 Authentication 은 SecurityContextHolder 에 설정됨

- ProviderManager : AuthenticationManager의 가장 일반적인 구현방식

- 


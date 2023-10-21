### SimpleUrlAuthenticationSuccessHandler

- 폼 기반 인증(Form-based authentication) 또는 기본적인 로그인 페이지를 사용하는 경우에 주로 사용됩니다.
- 사용자가 로그인에 성공하면, 지정된 URL로 리다이렉션하거나 특정 동작을 수행할 수 있습니다. 주로 사용자를 환영 메시지 페이지나 대시보드로 리다이렉션하는 데에 사용됩니다.

```java
public class CustomAuthenticationSuccessHandler extends SimpleUrlAuthenticationSuccessHandler {
    @Override
    public void onAuthenticationSuccess(HttpServletRequest request, HttpServletResponse response, Authentication authentication)
            throws IOException, ServletException {
        // 로그인 성공 후의 동작을 정의합니다.
        super.onAuthenticationSuccess(request, response, authentication);
    }
}

```





### OAuth2AuthorizationSuccessHandler

- OAuth 2.0 프로토콜을 기반으로 한 인증 프로세스에서 사용됩니다. OAuth 2.0은 외부 서비스(provider)를 사용하여 사용자를 인증하고 권한을 부여하는 프로토콜입니다.
- OAuth 2.0 흐름의 일부로서, OAuth 2.0 인가 코드가 성공적으로 교환되고 사용자가 인증되었을 때 실행되는 코드를 포함할 수 있습니다. 이 핸들러는 주로 외부 인증 공급자(예: Google, Facebook)와 연동할 때 사용됩니다.

```java
public class CustomOAuth2AuthorizationSuccessHandler implements OAuth2AuthorizationSuccessHandler {
    @Override
    public Mono<Void> onAuthorizationSuccess(OAuth2AuthorizationExchange exchange, Authentication authentication) {
        // OAuth 2.0 인증 성공 후의 동작을 정의합니다.
        return Mono.empty();
    }
}
```




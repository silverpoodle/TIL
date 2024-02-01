<img src="https://private-user-images.githubusercontent.com/88484476/301835179-ca6e6913-d1c3-47a2-be69-4ac28d5b5947.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDY4NzUxNTUsIm5iZiI6MTcwNjg3NDg1NSwicGF0aCI6Ii84ODQ4NDQ3Ni8zMDE4MzUxNzktY2E2ZTY5MTMtZDFjMy00N2EyLWJlNjktNGFjMjhkNWI1OTQ3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAyMDIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMjAyVDExNTQxNVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTA5ZmExNjE5NDFkNTlmNjY5NGU3Nzc5Mzk5Yjk5OThhYWU0YjRmYzdkZTQ3ZDFmNGUwOTlmZWEyZDNjZjA5ZjcmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.CEtc2a_ha7qUsul4CXHisId_LDSV8cA4yEq8pFYUm98" alt="image" style="zoom:50%;" />



**자바 언어를 위한 ORM(Object Relationship Mapping) 프레임워크**

=> JPA의 구현체로, JPA 인터페이스를 구현하며, 내부적으로 JDBC API를 사용

1. 관계형 데이터베이스와 객체의 패러다임 불일치 문제를 해결
2. 영속성 컨텍스트(엔티티를 영구 저정하는 환경) 제공





### JDBC(Java Database Connectivity) 

**데이터베이스와 통신하기 위한 API,  데이터베이스의 종류에 상관없이 똑같은 코드**



JDBC API는 설정한 데이터베이스에 맞는 드라이버를 사용하여 데이터베이스에 접근하기 때문이다.

즉, JDBC는 인터페이스이고 구현한 것은 각 데이터베이스에 맞는 드라이버들이다.







#### JPA(Java Persistence API)


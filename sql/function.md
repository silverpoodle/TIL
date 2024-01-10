### Math

- ABS(num): 절대값
- MOD(num A, num B): A % B
- CEILING(num): 소수점 올림
- FLOOR(num): 소수점 내림

- TRUNCATE(num A, num B): 소수점 B 번째부터 버림

- ROUND(num A, num B): 소수점 B 부터 반올림

<img src="/Users/jungin/Library/Application Support/typora-user-images/image-20240110191753833.png" alt="image-20240110191753833" style="zoom:50%;" />



- MIN(column)
- MAX(column)
- GREATEST(num A, numB ...)
- LEAST(num A, numB ...)
- SQRT(num) : 루트
- POW(num A, num B) : A의 B 제곱
- EXP(num) : e의 num 제곱
-  LOG(num) :자연로그
- SIN(PI() / 2): 삼각함수 sin
- COS(PI()): 삼각함수 cos
- TAN(PI() / 4): 삼각함수 tan
- RAND(): 0~1 사이 랜덤 숫자 생성





### String

- CHAR_LENGTH: 문자의 개수
- LENGTH: 할당된 byte 변환
- CONCAT('A', 'B', 'C'): 문자열 합치기, ABC
- REPEAT('A', n): 문자열 n번 반복
- LOCATE: 문자열 위치 찾음

```
LOCATE('abc', 'ababcDEFabc'); // 3
LOCATE('abc', 'ababcDEFabc', 4); // 9
```

- LEFT('text', num): 왼쪽 기준 num번째 개수만큼 뽑음
- RIGHT('text', num): 오른쪽 기준 num번째 개수만큼 뽑음

```
left('MySQL is an open source relational database management system', 5); -- MYSQL 
right('MySQL is an open source relational database management system', 6); -- system
```





### Date

- NOW()
- SYSDATE()
- CURRENT_TIMESTAMP()
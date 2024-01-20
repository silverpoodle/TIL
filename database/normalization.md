### 정규화 (normalization)

**`데이터의 중복으로 인하여 예상하지 못했던 문제가 발생하는 것을 방지하기 위해 스키마를 분해(decomposition) 하는 과정`**

![Normalization Process in DBMS - GeeksforGeeks](https://media.geeksforgeeks.org/wp-content/uploads/20200804110751/normalizationedited.jpg)

#### 1차 정규형

```
테이블 R 에 속한 모든 도메인이 원자값(atomic value) 만으로 구성되어 있는 경우
```

<img src="C:\Users\jungi\AppData\Roaming\Typora\typora-user-images\image-20240119225151315.png" alt="image-20240119225151315" style="zoom:50%;" />



#### 2차 정규형

```java
 제1 정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블을 분해한 경우
 /* 완전 함수 종속: 키의 부분 집합이 결정자가 되지 않음 (부분 종속 x) */
```



<img src="C:\Users\jungi\AppData\Roaming\Typora\typora-user-images\image-20240119230154978.png" alt="image-20240119230154978" style="zoom:50%;" />

=> 기본키가 '고객ID'와 '상품코드' 속성으로 구성되어있을 때 '제품명'은 기본키 중 '제품코드'만 알아도 식별 가능

 *이 경우에는 '제품명' 속성은 기본키에 **부분 함수 종속**된 관계*

=> 하지만, '수량' 속성은 기본키를 알아야 식별이 가능

*이 경우 '수량' 은 기본키에 **완전 함수 종속**된 관계*



#### 3차 정규형

```java
제2 정규화를 진행한 테이블에 대해 이행적 종속을 없애도록 테이블을 분해하는 것
 /* 이행적 종속:  X, Y, Z라는 3 개의 속성이 있을 때 X→Y, Y→Z 이란 종속 관계가 있을 경우, X→Z가 성립 */
```



<img src="C:\Users\jungi\AppData\Roaming\Typora\typora-user-images\image-20240119231103247.png" alt="image-20240119231103247" style="zoom:50%;" />

=> '제품코드' 로 '소분류' 를 알 수 있다.

=> '소분류' 로 '대분류' 를 알 수 있다.

=> 따라서 '제품코드' 로 '대분류' 를 알 수 있다. =  대분류는 소분류에 의해 관계되는 항목이지만, 제품코드를 통해 귀속



#### 보이스-코드 정규형(BCNF)

```java
제3 정규화를 진행한 테이블에 대해 모든 결정자가 후보키가 되도록 테이블을 분해한 경우
 /* 후보키:  테이블에서 각 행을 유일하게 식별할 수 있는 최소한의 속성들의 집합. 
            후보키는 기본키가 될 수 있는 후보들이며 유일성과 최소성을 동시에 만족 
    X → Y 일 때 X는 결정자, Y는 종속자  */
```



<img src="C:\Users\jungi\AppData\Roaming\Typora\typora-user-images\image-20240119232304769.png" alt="image-20240119232304769" style="zoom:50%;" />

=> (학생, 과목) -> 교수  &  교수 -> 과목

=> 교수가 과목을 결정하는 결정자이지만, 후보키가 아니라는 점



<img src="C:\Users\jungi\AppData\Roaming\Typora\typora-user-images\image-20240119233957133.png" alt="image-20240119233957133" style="zoom:50%;" />

=> 학생 / 교수 (함수적 종속x) , 교수 -> 과목



#### 역정규화

```
정규화를 거치면 릴레이션 간의 연산(JOIN 연산)이 많아지는데, 이로인해 성능이 저하
성능 문제가 있는(읽기작업이 많이 필요한) DB의 전반적인 성능을 향상시키기 위해 역정규화 진행
```

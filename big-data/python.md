# 빅데이터 실습

## 1. Local 환경

- 파이썬 설치, 필요한 라이브러리 (Numpy, Pandas, Scikit-learn 등) 설치
- IDE 설치 (Jupyter Notebook, VS code, Pycharm)
- 패키지 관리: **pip**



## 2. 가상 환경

- 개발 프로젝트별로 독립적인 가상 환경 생성, 프로젝트에 필요한 라이브러리 버전 관리
- **Anaconda**: 파이썬/라이브러리 등을 포함한 패키지 관리 & 가상 환경 관리
  - 프로젝트 간 의존성 충돌 방지, 환경 관리 효율적으로 수행
- **Colab**: 구글에서 제공하는 무료 웹 기반 개발 환경
  - 브라우저를 통해 코드 작성, 실행 가능
  - **GPU** 지원과 **협업** 기능 제공
  - 무료 사용 가능

<br/>

# Python 기초

## 1. 제어문

제어문은 프로그램의 흐름을 제어하는 역할
데이터를 처리하고 원하는 결과를 얻기 위해 사용

- **순차**: 코드가 작성된 순서에 따라 위에서 아래로 실행됩니다.
- **선택**: 조건에 따라 실행됩니다. 조건이 참이면 한 블록을, 거짓이면 다른 블록을 실행합니다.
- **반복**: 일정 조건이 참일 때 명령 블록을 반복 실행합니다.

---

### 1) 순차 구조
순차 구조는 코드가 작성된 순서대로 순차적으로 실행

```python
!pip3 install ColabTurtle
import ColabTurtle.Turtle as t
t.initializeTurtle()

# 7초를 맞추는 프로그램
import time
input("엔터를 누르기 7초를 기다리세요")
start = time.time()
input("7초라고 생각되면 엔터를 누르세요!")
end = time.time()
et = round(end - start, 2)
print(f"실제 시간: {et} 초")
print(f"차이 시간: {et - 7} 초")
```

- `time` 모듈을 사용하여 실제 시간과 입력 시간 차이를 계산

---

### 2) 선택 구조 (if 문)
선택 구조는 조건에 따라 다른 코드를 실행

```python
# 짝수, 홀수 판별
n = int(input("정수를 입력:"))
if n % 2 == 0:
    print(f"{n}은(는) 짝수입니다.")
else:
    print(f"{n}은(는) 홀수입니다.")

# 학점 계산
score = int(input("점수를 입력:"))
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'F'

print(f"당신의 점수는 {score}이고, 학점은 {grade}입니다.")
```

- `if-elif-else` 구조를 통해 조건에 따라 다른 학점을 출력

---

### 3) 반복 구조 (for, while 문)

#### 1. for 문
반복 구조는 특정 조건이 참인 동안 같은 코드를 반복 실행

```python
# for 문을 이용한 도형 그리기
t.initializeTurtle(10, (500, 300))
for n in range(5):
    t.fd(100) # 앞으로 100 픽셀 이동
    t.rt(144) # 오른쪽으로 144도 회전

# 0부터 3까지 출력
for a in range(4):
    print(a)

# 1부터 3까지 출력
for a in range(1, 4):
    print(a)

# 짝수 출력 (2 4 6 8 10)
for x in range(2, 11, 2):
    print(x)

# 홀수 출력 (1 3 5 7 9)
for x in range(1, 10, 2):
    print(x)

# 5의 배수 출력 (5 10 15 20 25 30 35 40 45 50 55 60 65 70 75 80 85 90 95 100)
for x in range(5, 101, 5):
    print(x, end=" ")
```

#### 2. while 문
while 문은 조건이 참일 동안 계속해서 실행됩니다.

```python
n = 0
while n < 4:
    print(n)
    n += 1
```

---

### 도형 그리기 프로그램

```python
# 사용자가 원하는 도형을 그리는 프로그램
while True:
    sides = int(input("그리고자 하는 도형 숫자를 입력(3~):"))
    if sides < 3:
        print("3 이상의 숫자를 입력해주세요.")
        continue
    for _ in range(sides):
        t.fd(100)
        t.lt(360 / sides)

    cont = input("계속 하시겠습니까? (yes or no): ")
    if cont.lower() != 'yes':
        print("--- 도형 그리기 종료!! ---")
        break
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241024094832881.png?raw=true" alt="image" style="zoom:100%;" />

---

### 무지개 그리기

```python
# ColabTurtle 초기화: 속도를 7로 설정하고, 창 크기를 (400, 200)으로 설정
t.initializeTurtle(7, (400, 200))

# 랜덤 색상을 사용하기 위한 random 모듈 임포트
import random

# 선의 두께 설정
t.width = 3

# 초기 선의 길이 설정
length = 10

# 선의 길이가 150보다 작을 때까지 반복
while length < 150:
    # 랜덤으로 RGB 색상 값 생성 (0~255 범위)
    r = random.randint(0, 255)
    g = random.randint(0, 255)
    b = random.randint(0, 255)
    
    # 거북이 색상 설정
    t.color(r, g, b)
    
    # 현재 길이만큼 앞으로 이동
    t.fd(length)
    
    # 오른쪽으로 89도 회전 (사각형 비슷한 패턴을 위해)
    t.rt(89)
    
    # 선의 길이를 5씩 증가
    length = length + 5
```

이 코드는 무작위 색상을 사용하여 점점 길어지는 선을 그리며, 89도씩 회전하면서 사각형 모양의 도형을 그리게 됩니다. 결과적으로 무지개 같은 색의 패턴!



<br/>

## 2. 변수 & 자료형

#### 1) 변수 (Variable)
데이터를 저장하는 **메모리 공간**에 이름을 붙인 것

- 변수 이름 규칙:
  - **문자**로 시작해야 하며, 숫자로 시작할 수 없음.
  - 특수문자는 **`_`**만 사용 가능.
  - 변수 이름은 의미 있게 부여하는 것이 좋음.

```python
a1 = 100
a2 = 3.14
name = "홍길동"
logic = True
print(f"a1의 값: {a1} a2의 값: {a2} name의 값: {name}")
print(f"logic의 값: {logic}")
```

#### 2) 자료형 (Data Type)
- **정수형** (`int`): 100
- **실수형** (`float`): 3.14
- **문자열** (`str`): "홍길동"
- **논리형** (`bool`): True, False

```python
print(type(a1))  # <class 'int'>
print(type(a2))  # <class 'float'>
print(type(name))  # <class 'str'>
print(type(logic))  # <class 'bool'>
```

#### 3) 연산자 (Operators)
파이썬에서 사용할 수 있는 연산자의 종류는 다음과 같습니다.

- **산술 연산자**: `+`, `-`, `*`, `/`, `//`(몫), `%`(나머지), `**`(거듭제곱)
- **관계 연산자**: `>`, `<`, `>=`, `<=`, `==`, `!=`
- **논리 연산자**: `and`, `or`, `not`

```python
print(5 / 4)  # 1.25
print(5 // 4)  # 1
print(5 % 4)  # 1
print(5 ** 4)  # 625
print(5 > 3 and 5 > 7)  # False
print(5 > 3 or 5 > 7)  # True
print(not(5 > 3 or 5 > 7))  # False
```

#### 4) 자료의 출력과 입력
- **`input()` 함수**로 사용자 입력을 받음.모든 입력은 **문자열**로 처리
- 숫자 입력이 필요할 때는 형변환(`int()`)을 사용해야 함

```python
name = input("이름을 입력해 주세요: ")
age = input("나이를 입력해 주세요: ")
print(type(age))  # <class 'str'>
age = int(age)  # 문자열을 정수로 변환
print(type(age))  # <class 'int'>
```

- 기본 `print()` 함수:
```python
print("이름은", name, "이고 나이는 내년에", age+1, "입니다.")
```

- 문자열 연결:
```python
print("이름은 " + name + "이고 나이는 내년에 " + str(age + 1) + "입니다.")
```

- **포맷팅 방식**:
  - `%` 포맷팅:
  ```python
  print("이름은 %s이고 나이는 내년에 %d입니다." % (name, age + 1))
  ```

  - **f-string**(권장):
  ```python
  print(f"이름은 {name}이고 나이는 내년에 {age + 1}입니다.")
  ```



<br/>

## 3. 문자열 다루기

#### 1) 문자열
- 문자열은 문자들의 시퀀스로, 단일따옴표(`'`) 또는 이중 따옴표(`"`)로 묶어 표현.
- 문자열의 **불변성**: 문자열은 한 번 생성되면 수정할 수 없으며, 수정하려면 새로운 문자열을 생성해야 함.

#### 2) 문자열 인덱싱
- 각 문자는 0부터 시작하는 인덱스를 가짐.
  ```python
  s1 = 'Hello, World!'
  first_char = s1[0]  # H
  w_char = s1[7]      # W
  ```

#### 3) 문자열 슬라이싱
- 문자열의 일부분을 추출할 수 있음.
  ```python
  print(s1[7:12])  # World
  print(s1[:5])    # Hello
  print(s1[7:])    # World!
  ```

#### 4) 문자열 연산
- 문자열 연결: `+`
- 문자열 반복: `*`
  ```python
  s3 = s1 + s2  # 'Hello, World!Python is fun.'
  s4 = "Python" * 5  # 'PythonPythonPythonPythonPython'
  ```

#### 5) 문자열 함수
- `len()`: 문자열 길이
- `upper()`: 대문자로 변환
- `lower()`: 소문자로 변환
- `find()`: 특정 문자열 찾기
- `replace()`: 문자열 대체
  ```python
  upper_s = s1.upper()  # 'HELLO, WORLD!'
  index = s1.find('World')  # 7
  replaced_s = s1.replace('World', 'PythonLove')  # 'Hello, PythonLove!'
  ```

#### 6) 문자열 포맷팅
- **f-문자열** 사용법:
  ```python
  name = 'Alice'
  print(f'Hello, {name}!')
  ```

#### 7) 문자열의 특수 문자
- **이스케이프 문자**: `\`
  ```python
  quote = "He said, \"Hello!\""
  print(quote) # He said, "Hello!"
  print("He said, \'Hello!\'") # He said, 'Hello!'
  print("He said, \\Hello!\\") # He said, \Hello!\
  ```



<br/>

## 4. 자료구조 다루기

#### 1) 리스트 (List)
- **정의**: 여러 데이터를 순차적으로 저장하는 자료구조, 대괄호 `[]`로 생성하며 **mutable**(변경 가능).
  ```python
  my_list = [1, 2, 3, 4, 5]
  mixed_list = [1, "apple", True, 3.14]
  ```

- **리스트 인덱싱 & 슬라이싱**
  
  ```python
  my_list = [10, 20, 30, 40]
  print(my_list[0]) #10
  print(my_list[2]) #30
  print(my_list[1:3]) # [20, 30]
  ```
  
  
  
- **리스트 컴프리헨션**: 리스트를 간결하게 생성할 수 있는 파이썬 문법.
  
  ```python
  squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
  ```
  
- **리스트 함수**: 
  
  ```python
  # 수정
  my_list[1] = 25 
  
  # append() - 리스트 끝에 요소 추가
  my_list = [1, 2, 3, 4, 5]
  my_list.append(6)
  print(my_list)  # [1, 2, 3, 4, 5, 6]
  
  # extend() - 리스트에 다른 리스트의 모든 요소 추가
  my_list.extend([7, 8])
  print(my_list)  # [1, 2, 3, 4, 5, 6, 7, 8]
  
  # insert() - 특정 위치에 요소 삽입
  my_list.insert(2, 10)
  print(my_list)  # [1, 2, 10, 3, 4, 5, 6, 7, 8]
  
  # remove() - 주어진 값과 일치하는 첫 번째 요소 삭제
  my_list.remove(10)
  print(my_list)  # [1, 2, 3, 4, 5, 6, 7, 8]
  
  # pop() - 인덱스를 지정해 요소 제거하고 그 값을 반환
  removed_item = my_list.pop(3)
  print(removed_item, my_list)  # 4 [1, 2, 3, 5, 6, 7, 8]
  
  # index() - 주어진 값과 일치하는 첫 번째 요소의 인덱스를 반환
  index = my_list.index(5)
  print(index)  # 3
  
  # count() - 리스트에서 주어진 값과 일치하는 요소의 개수 반환
  count = my_list.count(5)
  print(count)  # 1
  
  # sort() - 리스트 요소를 오름차순으로 정렬
  my_list.sort()
  print(my_list)  # [1, 2, 3, 5, 6, 7, 8]
  
  # reverse() - 리스트의 요소를 역순으로 정렬
  my_list.reverse()
  print(my_list)  # [8, 7, 6, 5, 3, 2, 1]
  
  # copy() - 리스트의 복사본 생성
  copied_list = my_list.copy()
  print(copied_list)  # [8, 7, 6, 5, 3, 2, 1]
  ```

- list & for

  ```python
  import random
  xlist = []
  for x in range(10) :
      n = random.randint(1, 10)
      xlist.append(n)
      print(xlist)
  
  [5]
  [5, 9]
  [5, 9, 10]
  [5, 9, 10, 3]
  [5, 9, 10, 3, 3]
  [5, 9, 10, 3, 3, 9]
  [5, 9, 10, 3, 3, 9, 9]
  [5, 9, 10, 3, 3, 9, 9, 5]
  [5, 9, 10, 3, 3, 9, 9, 5, 1]
  [5, 9, 10, 3, 3, 9, 9, 5, 1, 2]
  ```

  

#### 2) 튜플 (Tuple)

- 여러 값을 순서대로 저장하는 **불변** 자료구조, 소괄호 `()` 사용.
  ```python
  my_tuple = (1, 2, 3, 4)
  ```

- **특징**: 튜플은 **한 번 생성되면 변경할 수 없으며**, 메모리 효율이 좋고 빠름.

  ```python
  sorted_tuple = sorted(my_tuple)  # 리스트 반환
  ```

- **튜플의 활용 사례**: 함수에서 여러 값을 반환할 때, 변경되지 않는 데이터, 딕셔너리의 키로 사용 가능.

-  **zip() 함수**: 여러 이터러블 객체의 동일한 인덱스에 위치한 요소들을 묶어 튜플로 반환.

  ```python
  names = ('Alice', 'Bob', 'Charlie')
  ages = (25, 30, 35)
  people = tuple(zip(names, ages))  # (('Alice', 25), ('Bob', 30), ('Charlie', 35))
  ```

- **enumerate() 함수**: 이터러블 객체의 각 요소와 인덱스를 반환. 각 항목은 `(인덱스, 값)` 형태의 튜플.

  ```python
  # map() 함수는 이터러블의 각 요소에 대해 지정된 함수를 적용한 결과를 반환
  my_tuple = (1, 2, 3, 4)
  def square(n):
  	return n ** 2
  result = map(square, my_tuple)
  print(list(result)) # [1, 4, 9, 16]
  
  enumerated_list = list(enumerate(my_list))
  ```

  

- **map() 함수**: 이터러블의 각 요소에 지정된 함수를 적용한 결과 반환.

  ```python
  result = map(square, my_tuple)  # [1, 4, 9, 16]
  
  my_list = [1.3, 1.7]
  result = map(int, my_list )
  print(tuple(result))
  ```

- **lambda 함수**: 익명 함수 정의. 간단한 표현식을 빠르게 정의할 때 유용.

  ```python
  my_list = [(1, 'apple'), (3, 'banana'), (2, 'cherry')]
  sorted_list = sorted(my_list, key=lambda x: x[0])
  print(sorted_list) # [(1, 'apple'), (2, 'cherry'), (3, 'banana')]
  
  squared_tuple = tuple(map(lambda x: x**2, my_tuple))  # (1, 4, 9, 16)
  ```




#### 3) Dictionary

- key-value 쌍으로 데이터를 저장하는 자료구조

- 해시 테이블을 기반으로 구현, 빠른 검색/삽입/삭제 가능

  ```python
  my_dict =  {'name': 'Alice', 'age': 25}
  ```

- **생성 & 키 접근**

  ```python
  # 딕셔너리 생성과 키와 값의 접근
  phone = {}
  phone['강감찬'] = '010-760-1111'
  phone['홍길동'] = '010-760-2222'
  print(phone) # {'강감찬': '010-760-1111', '홍길동': '010-760-2222'}
  
  phone1 = {'김유신':'010-760-1212'}
  print(phone1) # {'김유신': '010-760-1212'}
  
  phone.update(phone1)
  print(phone) # {'강감찬': '010-760-1111', '홍길동': '010-760-2222', '김유신': '010-760-1212'}
  print(phone.get('홍길동')) # 010-760-2222
  print(phone['홍길동']) # 010-760-2222
  print(phone.keys()) # dict_keys(['강감찬', '홍길동', '김유신'])
  print(phone.values()) #dict_values(['010-760-1111', '010-760-2222', '010-760-1212'])
  
  # Sort 활용
  for key in sorted(phone.keys()) :
  	print(key, phone[key])  
      #강감찬 010-760-1111
  	#김유신 010-760-1212
  	#홍길동 010-760-2222
  
  # 삭제
  del phone['홍길동']
  print(phone) # {'강감찬': '010-760-1111', '김유신': '010-760-1212'}
  
  # 딕셔너리에서 주어진 키에 대한 값의 반환 함수 get()
  my_dict = {'name': 'Alice', 'age': 25}
  print(my_dict.get('name', 'Unknown')) # 'Alice' 출력
  print(my_dict.get('gender', 'Unknown')) # 키가 딕셔너리에 없는 경우 기정한 기본값 반환
  
  # 딕셔너리 생성과 키값의 순회
  my_dict = {'name': 'Alice', 'age': 25}
  for key in my_dict.keys():
  	print(key) 
      # name
      # age
  
  # 딕셔너리 값의 반환 함수 values()
  my_dict = {'name': 'Alice', 'age': 25}
  for value in my_dict.values():
  	print(value)
  	# Alice
      # 25
   
  # 특정 키가 딕셔너리에 있을 때만 삭제
  my_dict = {'a': 1, 'b': 2, 'c': 3}
  key_to_remove = 'd'
  
  if key_to_remove in my_dict:
  	del my_dict[key_to_remove]
  	print(f"{key_to_remove} 키가 삭제되었습니다.")
  else:
  	print(f"{key_to_remove} 키가 존재하지 않습니다.")
  	print(my_dict)
  	# d 키가 존재하지 않습니다.
  	# {'a': 1, 'b': 2, 'c': 3}
  ```

<br/>

#### 5) Set

- 중복 허용하지 않음 - 동일한 값 여러번 저장하지 않음

- 순서가 없는 고유한 값들의 모임

  - 인덱싱 / 슬라이싱 불가능
  - 집합과 비슷한 성질

  ```python
  a_set = {1, 2, 3}
  b_set = set([4, 5, 6])
  ```

- **생성 및 특징**

  ```python
  my_list = [1, 2, 2, 3, 4, 4, 5]
  x_items = set(my_list)
  print(x_items) # {1, 2, 3, 4, 5}
  
  # 세트에 새로운 원소를 추가 add()
  my_set = {10, 20, 30}
  my_set.add(5)
  print(my_set) # {10, 20, 5, 30}
  
  # 삭제 remove(), 삭제 원소 없을 시 KeyError 발생
  my_set = {10, 20, 30}
  my_set.remove(20)
  #my_set.remove(40)
  print(my_set) # {10, 30}
  
  # 삭제 discard(), 삭제 원소 없어도 오류 발생하지 않음
  my_set = {10, 20, 30}
  my_set.discard(20)
  my_set.discard(40)
  print(my_set) # {10, 30}
  
  set1 = {1, 2, 3}
  set2 = {3, 4, 5}
  set3 = set1.union(set2)
  set4 = set1.intersection(set2)
  set5 = set1.difference(set2)
  set6 = set2.difference(set1)
  print(set3) # {1, 2, 3, 4, 5}
  print(set4) # {3}
  print(set5) # {1, 2}
  print(set6) # {4, 5}
  ```

  
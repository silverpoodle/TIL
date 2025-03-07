# Numpy

1. **주요 특징:**
- 다차원 배열 객체(ndarray)를 효율적으로 다룰 수 있는 라이브러리
- C언어로 구현되어 있어 매우 빠른 연산 속도를 제공
- 메모리를 효율적으로 사용하며, 벡터화 연산을 지원
- 선형대수, 푸리에 변환, 난수 생성 등 다양한 수학적 기능을 제공

<br/>

2. **배열 생성:**
```python
import numpy as np

# 리스트로부터 배열 생성
arr1 = np.array([1, 2, 3, 4, 5])

# 0으로 채워진 배열 생성
zeros = np.zeros((3, 4))  # 3x4 배열

# 1로 채워진 배열 생성
ones = np.ones((2, 3))    # 2x3 배열

# 특정 범위의 배열 생성
range_arr = np.arange(0, 10, 2)  # [0, 2, 4, 6, 8]

# 균등 간격의 배열 생성
linspace = np.linspace(0, 1, 5)  # 0부터 1까지 5개의 균등 간격 숫자

# 랜덤 배열 생성
random_arr = np.random.rand(3, 3)  # 3x3 랜덤 배열
```

<br/>

3. **배열 연산:**

```python
# 기본 연산
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# 덧셈
print(a + b)  # [5, 7, 9]

# 곱셈
print(a * b)  # [4, 10, 18]

# 브로드캐스팅 (다른 형태의 배열 간 연산)
c = np.array([[1, 2, 3],
              [4, 5, 6]])
print(c + 1)  # 모든 원소에 1을 더함

# 통계 연산
print(np.mean(c))    # 평균
print(np.sum(c))     # 합계
print(np.max(c))     # 최대값
print(np.min(c))     # 최소값

# 행렬 연산
d = np.array([[1, 2], [3, 4]])
e = np.array([[5, 6], [7, 8]])
print(np.dot(d, e))  # 행렬 곱
```



<br/>

4. **리스트와 비교**

   NumPy 배열과 Python 리스트의 차이점을 상세히 비교해드리겠습니다:

   - 벡터화 연산 여부

   ```python
   # NumPy 배열: 벡터화 연산 가능
   np_array = np.array([1, 2, 3])
   print(np_array * 2)  # [2 4 6]
   
   # Python 리스트: 벡터화 연산 불가능
   py_list = [1, 2, 3]
   print(py_list * 2)   # [1, 2, 3, 1, 2, 3] (리스트 반복)
   ```

   - 데이터 타입

   ```python
   # NumPy 배열: 동일한 데이터 타입만 저장 가능
   np_array = np.array([1, 2, 3])  # 모든 요소가 int64 타입
   
   # Python 리스트: 다양한 데이터 타입 저장 가능
   py_list = [1, "hello", 3.14]  # 정수, 문자열, 실수 혼합 가능
   ```

   - 다차원 데이터 지원

   ```python
   # NumPy 배열: 효율적인 다차원 연산 지원
   np_2d = np.array([[1, 2], [3, 4]])
   print(np_2d[0, 1])  # 2
   
   # Python 리스트: 중첩 리스트로 구현
   py_2d = [[1, 2], [3, 4]]
   print(py_2d[0][1])  # 2
   ```

   - 크기 변경

   ```python
   # NumPy 배열: reshape 메서드로 쉽게 변경
   np_array = np.array([1, 2, 3, 4])
   reshaped = np_array.reshape(2, 2)
   
   # Python 리스트: 크기 변경을 위해선 직접 구현 필요
   # 별도의 reshape 기능 없음
   ```

   - 메모리 사용

     - NumPy 배열: 연속된 메모리 블록에 저장, 메모리 효율적

     - Python 리스트: 각 요소가 별도의 객체로 저장되어 더 많은 메모리 사용


   - 성능 비교

   ```python
   # NumPy 배열: 대규모 수치 연산에서 매우 빠름
   np_array = np.array([1, 2, 3, 4, 5])
   %timeit np_array * 2  # 매우 빠른 연산
   
   # Python 리스트: 반복문 필요로 더 느림
   py_list = [1, 2, 3, 4, 5]
   %timeit [x * 2 for x in py_list]  # 상대적으로 느린 연산
   ```

   - 제공 함수
     NumPy 배열:

     - 수학적 연산: np.sum(), np.mean(), np.std()

     - 행렬 연산: np.dot(), np.cross()

     - 차원 조작: reshape(), transpose()

     - 통계 함수: percentile(), variance()

     - 선형 대수: linalg 모듈

     - 푸리에 변환: fft 모듈

       


   - Python 리스트:

     - 기본 연산: append(), extend(), pop()

     - 정렬: sort(), reverse()

     - 검색: index(), count()

     - 추가/삭제: insert(), remove()

     - len() 함수로 길이 확인


<br/>

5. **인덱싱과 슬라이싱**

NumPy 배열의 인덱싱과 슬라이싱 방법을 자세히 설명해드리겠습니다:

- 기본 인덱싱

```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5])

# 단일 요소 접근
print(arr[0])     # 1
print(arr[-1])    # 5 (마지막 요소)

# 다차원 배열 인덱싱
arr_2d = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
                   
print(arr_2d[0, 0])   # 1
print(arr_2d[1, 2])   # 6
```

- 기본 슬라이싱

```python
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# 시작:끝:간격
print(arr[2:7])     # [3, 4, 5, 6, 7]
print(arr[::2])     # [1, 3, 5, 7, 9]
print(arr[1:8:2])   # [2, 4, 6, 8]
print(arr[::-1])    # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

- 다차원 배열 슬라이싱

```python
arr_2d = np.array([[1, 2, 3, 4],
                   [5, 6, 7, 8],
                   [9, 10, 11, 12]])

# 행, 열 슬라이싱
print(arr_2d[0:2, 1:3])    # [[2, 3],
                           #  [6, 7]]

# 모든 행의 특정 열 선택
print(arr_2d[:, 1])        # [2, 6, 10]

# 특정 행의 모든 열 선택
print(arr_2d[1, :])        # [5, 6, 7, 8]
```

- 불리언 인덱싱

```python
arr = np.array([1, 2, 3, 4, 5])

# 조건에 맞는 요소 선택
print(arr > 3)             # [False False False True True]
print(arr[arr > 3])        # [4, 5]

# 복합 조건
print(arr[(arr > 2) & (arr < 5)])  # [3, 4]
```

- 팬시 인덱싱

```python
arr = np.array([10, 20, 30, 40, 50])

# 인덱스 배열을 사용한 선택
indices = [1, 3, 4]
print(arr[indices])        # [20, 40, 50]

# 2차원 예시
arr_2d = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
                   
rows = [0, 2]
cols = [0, 2]
print(arr_2d[rows, cols])  # [1, 9]
```

- 뷰와 복사

```python
arr = np.array([1, 2, 3, 4, 5])

# 뷰 생성 (원본 데이터 공유)
view = arr[1:4]
view[0] = 10
print(arr)  # [1, 10, 3, 4, 5]

# 복사 생성 (독립적인 데이터)
copy = arr[1:4].copy()
copy[0] = 20
print(arr)  # [1, 10, 3, 4, 5] (원본 변경되지 않음)
```




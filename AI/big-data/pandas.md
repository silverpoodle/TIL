# Pandas

1. **주요 특징**
- 데이터 분석과 조작을 위한 파이썬 라이브러리
- NumPy를 기반으로 구축되어 고성능 처리 가능
- 엑셀과 유사한 데이터 처리 기능 제공
- Series(1차원)와 DataFrame(2차원) 두 가지 주요 데이터 구조 제공



<br/>

2. **Series 생성**
```python
import pandas as pd

# 리스트로부터 생성
s = pd.Series([1, 2, 3, 4, 5])

# 딕셔너리로부터 생성
dict_data = {'a': 1, 'b': 2, 'c': 3}
s = pd.Series(dict_data)

# 인덱스 지정
s = pd.Series([1, 2, 3], index=['a', 'b', 'c'])
```

<br/>

3. **DataFrame 생성**

```python
# 딕셔너리로부터 생성
df = pd.DataFrame({
    'name': ['John', 'Jane', 'Bob'],
    'age': [25, 30, 35],
    'city': ['NY', 'LA', 'SF']
})

# 리스트로부터 생성
data = [['John', 25, 'NY'], ['Jane', 30, 'LA']]
df = pd.DataFrame(data, columns=['name', 'age', 'city'])
```

<br/>

4. **DataFrame으로 파일 읽기**

```python
# CSV 파일 읽기
df = pd.read_csv('file.csv')

# Excel 파일 읽기
df = pd.read_excel('file.xlsx')

# JSON 파일 읽기
df = pd.read_json('file.json')
```

<br/>

5. **DataFrame의 조작**

```python
# 새로운 열 추가
df['new_column'] = [1, 2, 3]

# 열 삭제
df.drop('column_name', axis=1, inplace=True)

# 열 이름 변경
df.rename(columns={'old_name': 'new_name'}, inplace=True)

# 결측치 처리
df.fillna(0)  # 0으로 채우기
df.dropna()   # 결측치 있는 행 삭제
```

<br/>

6. **데이터 선택 loc (라벨 기반)**

```python
# 단일 행 선택
df.loc['row_label']

# 여러 행과 열 선택
df.loc['row_label', 'column_label']
df.loc['row1':'row3', 'col1':'col3']
```

<br/>

7. **데이터 선택 iloc (위치 기반)**

```python
# 단일 행 선택
df.iloc[0]

# 여러 행과 열 선택
df.iloc[0:3, 0:2]
df.iloc[[0, 2, 4], [1, 3]]
```

<br/>

8. **조건을 이용한 선택**

```python
# 단일 조건
df[df['age'] > 25]

# 복합 조건
df[(df['age'] > 25) & (df['city'] == 'NY')]
```

<br/>

9. **타입의 변환**

```python
# 문자열을 날짜로 변환
df['date'] = pd.to_datetime(df['date'])

# 데이터 타입 변환
df['number'] = df['number'].astype('int64')
```

<br/>

10. **사칙연산**

```python
# 열 간의 연산
df['sum'] = df['col1'] + df['col2']
df['multiply'] = df['col1'] * df['col2']

# 열에 스칼라값 연산
df['col1'] = df['col1'] * 2
```

<br/>

11. **주요 함수들**

```python
# 기본 통계
df.describe()     # 기술통계량
df.mean()         # 평균
df.median()       # 중앙값
df.max()          # 최대값
df.min()          # 최소값

# 그룹화
df.groupby('category').mean()

# 정렬
df.sort_values('column_name')

# 중복 제거
df.drop_duplicates()
```

<br/>

12. **Pandas와 시각화**

```python
# 기본 플롯
df.plot()

# 다양한 차트 유형
df.plot(kind='bar')     # 막대 그래프
df.plot(kind='scatter') # 산점도
df.plot(kind='box')     # 박스 플롯
df.plot(kind='pie')     # 파이 차트

# matplotlib과 함께 사용
import matplotlib.pyplot as plt
df.plot()
plt.show()
```


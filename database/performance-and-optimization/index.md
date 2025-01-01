### Index

**`데이터베이스의 테이블에 대한 검색 속도를 향상시켜주는 자료구조`**

**` => 레코드에 대한 검색 속도를 높이기 위해 물리적 저장 위치를 별도로 기록함`**

<img src="https://user-images.githubusercontent.com/38887077/76482821-4ec64780-6450-11ea-862e-da506f5cdae2.png" alt="How Indexing Works in NebulaGraph" style="zoom: 33%;" />

Pros

```
- 테이블을 검색하는 속도와 성능이 향상
- 시스템의 전반적인 부하를 줄일 수 있다. 
```

Cons

```
1. 인덱스를 관리하기 위한 추가 작업이 필요
2. 추가 저장 공간 필요
3. 잘못 사용하는 경우 오히려 검색 성능 저하
```



#### Hash Table

<img src="https://blog.kakaocdn.net/dn/y0OIg/btrwn4Ybex8/1JeiDurjQlIcvDC36zRM30/img.webp" alt="img" style="zoom:50%;" />

-  데이터 요소의 주소/인덱스 값이 해시 함수에서 생성
- 키는 해싱 함수를 통해 생성
  - 키 값 자체가 데이터를 저장하는 배열의 인덱스가 되기 때문에 데이터 요소의 검색 및 삽입 기능 향상
- 시간 복잡도는 O(1)
- **등호(=) 연산**에만 **특화**   -> '단 하나'의 데이터를 찾을 
  - 해시 함수는 값이 조금이라도 달라지면 완전히 다른 해시 값을 생성
  - 부등호 연산(>, <)이 자주 사용되는 데이터베이스 검색을 위해서는 해시 테이블이 부적합



#### B- Tree

![img](https://blog.kakaocdn.net/dn/cDLSvr/btrasTRTsZV/Bim8K9iPSSTKNdQpPMtUQ1/img.jpg)

-  노드하나에 여러 데이터를 저장
- **branch 노드에 key와 data를 담는 형식**
- 시간복잡도는 O(log N)
- 노드안의 배열은 항상 정렬된 상태로 있어 부등호 연산 가능
- 노드의 개수를 늘리고 트리의 전체 높이를 줄여서 빠른 탐색 속도



#### B+ Tree

<img src="https://blog.kakaocdn.net/dn/bRiL19/btqBTMSBCWF/J3nKw2qympUVxGThnVdLK0/img.png" alt="img" style="zoom:50%;" />

- B-tree의 확장개념, **브랜치 노드에 key만 담아두고, data는 담지 않음**
  - **`리프 노드에만 key와 data를 저장하고, 리프 노드끼리 Linked list로 연결 `**
- 메모리를 더 확보함으로써 더 많은 key들을 수용
  - 하나의 노드에 더 많은 key들을 담을 수 있기에 트리의 높이는 더 낮아짐
-  풀 스캔 시  리프 노드에 데이터가 모두 있기 때문에 한 번의 선형탐색만 하면 됨. B-tree의 경우에는 모든 노드를 확인해야 함\



> `명칭 참고 ><  (루트 노드 - 브랜치 노드 - 리프 노드)`

<img src="https://blog.kakaocdn.net/dn/qycZ2/btqBQnr4QYG/7J8KpnmNaJiTjgS0K9TEIK/img.png" alt="img" style="zoom: 80%;" />

https://zorba91.tistory.com/293        -> 정리가 잘 되어있는 블로그입니당^^

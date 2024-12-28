# Open Source License

`SW 에 대한 허가권, 사용/복제/수정/배포 가능`

### 1. 종류

MIT > GNU (GPL 2.0) > Apache > GNU (GPL 3.0) > BSD 2.0 > ISC ...



<br/>

### 2. 공통 준수 사항

1. 저작권 관련 문구 유지
   - 저작권 표시의 의무
   - LGPL 에 의해 배포된다는 사실 명시
   - 보증 책임이 없다는 표시
   - 저작권자의 연락처
2. 제품명 중복 방지
3. 서로 다른 라이선스의 조합
   - 서로 다른 라이선스 사용 경우 상충하지 안흔ㄴ지 확인
   - **Compatibility(양립성) 문제**

<br/>

### 3. 라이선스 별 상이한 의무사항

1. 사용 여부 명시 
   - 명시 요구 : GPLv2, GPLv3, LGPL 2.1, MPL
   - 명시 요구 없음: BSD, MIT, EPL, CPL
2. **소스 코드 공개**
   - 수정/추가한 부분에 대한 소스코드 명시
   - **GPL**
3. 특허
   - Patent Grant: Licensor 가 특허권 가진 경우 OSS 와 함께 무상으로 제공
   - Patent Retaliation: Licensee 가 특허권 가진 경우 침해 소성을 제기할 수 없음

<br/>

### 4. 라이선스 분류

- Copyright: 저작물 보호, 사용자가 저작가의 허가 받아야 함
- Copyleft: 저작물 자유롭게 사용 가능, 변경된 소스 코드는 공개해야함

#### PERMISSIVE  <---------------------------------------> RESTRICTIVE

**Give Me credit > Give Me Fixes (weak copyleft) > Give me everything (strong copyleft)**

1. GMC: BSD, MIT, Apache : 수정 시 소스코드 공개 의무 X
2. GMF: LGPL, MPL, EPL
3. GME: GPL, Affero GPL



<br/>

### 4. 라이선스 양립성 (Compatibility)

`서로 다른 의무사항을 가진 공개 SW 라이선스는 의무사항 충돌로 인해 양립이 불가능한 경우 발생 가능. 양립 불가능시 배포 불가능`

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241021204348695.png?raw=true" alt="image-20240218203439687" style="zoom:50%;" />

<br/>

### 4. 이중 라이선스 (Dual)

`원래의 라이선스 외에 예외적 사용을 허가하는 라이선스, 개발자는 유리한 라이선스를 선택하여 사용 가능`

<br/>

### 5. 라이선스 위반 모니터링

- 위반 감시 단체
  - FSF
  - gps-violations.org
  - SFLC
  - KOSS Law Center



<br/>

### 6. 라이선스 관리 방안 (governanace)

- **라이선스 관리**: 관리 기획 -> 관리 -> 검증 -> 보고서 작성/공유
- **SW 개발**: 분석/설계 -> 구현 -> 테스트 -> 릴리스
  - 분석/설계: 어떤 SW 활용? 양립성?
  - 구현: SW 사용 목록 작성, 레포지토리 저장
  - 테스트: Protex, Fossology 등 검증 도구
  - 릴리스: 소스코드 공개, 사용여부 명시
# JaCoCo

<img src="https://about.codecov.io/wp-content/uploads/2020/11/jacoco-logo.png" alt="Do" style="zoom:80%;" />

#### Java 프로젝트의 코드 커버리지를 측정하기 위한 오픈소스 라이브러리로, 테스트가 소스 코드의 어느 부분을 실행했는지 분석

- 💡테스트 실행 중 코드 커버리지 데이터를 수집하고, HTML, XML, CSV와 같은 다양한 형식으로 리포트를 생성💡
  - 실행된 **코드 라인 수**와 **조건문(브랜치)**의 실행 여부를 평가
  - 별도의 코드 변경 없이 JVM에 JaCoCo 에이전트를 추가하여 테스트 데이터를 수집





<br/>

## 1. 사용 방법



### 1.1 Gradle 프로젝트에서 JaCoCo 플러그인 추가

```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.3'
    id 'io.spring.dependency-management' version '1.1.4'
    id 'jacoco'
}

group = 'com.runninghi'
version = '0.0.1-SNAPSHOT'
jar.enabled = false

java {
    sourceCompatibility = '17'
}

jacoco {
    toolVersion = "0.8.8"
}

jacocoTestReport {
    reports {
        html {
            enabled true // HTML 형식의 코드 커버리지 리포트 생성 활성화
        }
        xml {
            enabled true // XML 형식의 코드 커버리지 리포트 생성 활성화
        }
    }
    // QueryDSL QDomain 클래스 제외
    def QDomains = ('A'..'Z').collect { "**/Q${it}*" } // QDomain 파일 패턴 설정

    afterEvaluate {
        // 코드 커버리지 측정 시 제외할 디렉터리와 파일 설정
        classDirectories.setFrom(
                files(classDirectories.files.collect {
                    fileTree(dir: it, excludes: [
                            "**/*Application*", 
                            "**/entity/**", 
                            "**/enumtype/**", 
                            "**/repository/**", 
                            "**/aop/**",    
                            "**/apple/**", 
                            "**/constant/**", 
                            "**/converter/**", 
                            "**/version/**",     
                            "**/config/**",      
                            "**/dto/**",         
                    ])
                })
        )
    }
    finalizedBy jacocoTestCoverageVerification // 리포트 생성 후 테스트 커버리지 검증 실행
}

jacocoTestCoverageVerification {
    violationRules {
        rule {
            limit {
                minimum = 0.3 // 코드 커버리지 최소 허용 비율(30%)
            }
        }
    }
}

tasks.named('test') {
    useJUnitPlatform() // JUnit Platform 사용
    finalizedBy 'jacocoTestReport' // 테스트 완료 후 JaCoCo 리포트 생성 실행
}
```



<br/>

### 1.2  커버리지 기준 설정

- `jacocoTestCoverageVerification` 태스크를 사용하여 Jacoco 규칙을 설정

- **`enabled`**: JaCoCo의 특정 기능(리포트 형식)을 활성화할지 여부를 결정

  - `html { enabled true }`는 HTML 형식 리포트를 활성화하여 브라우저로 볼 수 있는 리포트를 생성
  - `xml { enabled true }`는 XML 형식 리포트를 활성화하여 CI/CD 파이프라인에서 분석할 수 있도록 함

- **`element`**: JaCoCo가 커버리지 리포트를 생성할 때 분석하는 코드 구성 요소

  - 일반적으로 **라인(line)**, **브랜치(branch)**, **클래스(class)**와 같은 단위로 구성됨
  - EX. 리포트에는 각 클래스, 메소드, 라인에 대한 커버리지 상태가 포함됨.
    

- **`count`**: 특정 `element`의 실행 횟수를 나타냄.

  - **라인(Line)**: 코드의 한 줄이 실행된 횟수.
  - **브랜치(Branch)**: 조건문에서 `true` 또는 `false`로 실행된 횟수.
  - **클래스(Class)**: 클래스 내의 메소드들이 실행된 횟수.

  <br/>

``` groovy
jacocoTestCoverageVerification {
    violationRules {
        // 규칙 1: 전체 코드 커버리지 최소 허용 비율 설정
        // 각 클래스에서 80% 이상의 코드 라인이 실행되어야 빌드 성공
        // 클래스 A: 85% → 성공!
	   // 클래스 B: 75% → 실패
        rule {
            element = 'CLASS' // 클래스 단위로 커버리지 체크
            limit {
                counter = 'LINE' // 커버리지 계산 기준: 코드 라인
                value = 'COVERED_RATIO' // 기준 값: 커버된 비율
                minimum = 0.8 // 커버리지 최소값: 80%
            }
        }
        
        // 규칙 2: 조건문(branch) 커버리지 설정
        // 각 메소드 내 조건문(branch)에서 최소 하나의 분기가 실행되어야 성공
        // 메소드 doSomething(): 조건문 2개 → 실행된 브랜치 1개 → 성공!
        // 메소드 calculate(): 조건문 3개 → 실행된 브랜치 0개 → 실패

        rule {
            element = 'METHOD' // 메소드 단위로 커버리지 체크
            limit {
                counter = 'BRANCH' // 커버리지 계산 기준: 브랜치 (조건문)
                value = 'COVERED_COUNT' // 기준 값: 커버된 갯수
                minimum = 1 // 모든 조건문에 대해 최소 하나의 브랜치를 커버해야 함
            }
        }
    }
}
```

<br/>

```kotlin
Rule violated for class com.example.MyClass: 
  Lines covered ratio is 0.75, but the minimum is 0.8.
Rule violated for method com.example.MyMethod: 
  Branches covered count is 0, but the minimum is 1.
```

<br/><br/>

## 2. 고민할 점

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20250126220846330.png?raw=true" alt="image-20250126220846330" style="zoom:80%;" />

- 러닝하이에 적용해봤을때 이지럴이 났다.. 32%!?!?!?!? ㅁㅊ갯다 분발하쟈

> 🤔100% 커버리지를 목표로 해야할까🤔

#### ✅ 높은 테스트 커버리지의 이점

- 테스트 100% 보장 -> 부담없는 배포가 가능해짐
- 테스트 필요성이 없어지는 코드를 바로 제거
- 이미 작성한 테스트를 참고해 새 테스트를 더 빠르게, 점점 쉬워지는 테스트 작성

<br/>

#### ⚠️ 높은 테스트 커버리지 주의점

- 테스트는 빨리야 함 -> 테스트가 느려지면 생산성이 떨어진다
- 커버리지가 100%라도, 버그는 존재



























<br/><br/>

참고

https://velog.io/@kimsei1124/JaCoCo-%ED%99%9C%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0

https://techblog.woowahan.com/2661/

https://toss.im/slash-21/sessions/1-6    

https://medium.com/byungkyu-ju/toss-slash21-%ED%85%8C%EC%8A%A4%ED%8A%B8%EC%BB%A4%EB%B2%84%EB%A6%AC%EC%A7%80-100-%EC%9A%94%EC%95%BD-demo-2fb8b52cf2a9
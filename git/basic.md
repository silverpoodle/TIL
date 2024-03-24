- **프로젝트를 진행할 때 보여주고 싶지 않은 민감 정보를 담은 yml 파일이 존재**
- **submodule을 사용하여 특정 폴더만 private로 설정하여 노출을 막음**

</br>

### 과정

1. **public repository에 프로젝트 파일 업로드**

2. **민감한 정보를 담을 private repository 생성**

   1. application.yml 파일을 private repository에 생성하여 추가
   2. public repository에 존재하는 민감한 정보를 private repository로 옮기고 clone 시에만 연동해서 가져온다고 생각하면 된다.

3. **public repository에 submodule 등록**

   ```bash
   git submodule add 서브모듈로 등록할 github repo 주소
   
   ex) git submodule add <https://github.com/~~~>
   ```

   - 위 명령어로 등록하면 프로젝트의 최상위 경로에 submodule의 repository name을 가진 폴더가 생성된다.

4. **.gitmodules 확인**

   1. 위 과정을 거치면 프로젝트 최상위 폴더에 .gitmodules 파일이 생성된다.
   2. .gitmodules 파일은 submodule repo의 경로와 url을 알려준다.
   3. 메인 프로젝트를 github에 push 하면 main 프로젝트(public repository)에 submodule(private repository)가 생성된다.
   4. public repository더라도 위 submodule 폴더는 private repository 권한이 없는 유저는 접근 불가

5. **submodule의 파일이 수정되었다면?**

   ```bash
   git submodule update --remote
   ```

   - 위 명령어를 통해서 submodule의 최신 내용을 메인 프로젝트에 갱신할 수 있다.
   - main project를 새로 clone 하였을 경우에도 위 명령어를 통해서 submodule을 받아올 수 있다.

6. **gradle을 submodules의 내용을 빌드 시 가져오기**

   1. submodules 폴더에 있는 yml 파일들을 빌드 시에 “프로젝트 명/src/main/resources” 경로로 가져오게 하는 작업이 필요하다.
   2. build.gradle에 아래 코드 추가

   ```java
   task copyPrivate(type: Copy) {
   	copy{
   			from 'submodule폴더'
   			include "application.yml"
   			into 'src/main/resources'
   	}
   }
   ```

   from : submodule 의 폴더

   - 아마 우리 프로젝트에서는 ‘./config-repo’ 가 될 듯

   include : 포함할 파일

   into : 빌드 시에 넣을 경로

   - gradle이 copyPrivate task를 수행할 때 from 경로의 repo에 있는 `application.yml` 파일을 메인 프로젝트의 `src/main/resources` 에 복사하라는 의미
   - 위 작업 후에 bulid.gradle refresh 필수!!
   - intellij 의 오른쪽 바에서 Gradle → Tasks → other → copyPrivate 를 실행

- 수정 사항이 있는 경우
  - 아래 코드를 터미널에 입력하고 copyPrivate task를 실행해주면 된다.
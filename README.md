# codyssey-m1
코디세이 AI 올인원 입학연수과정 미션1

### 1. 프로젝트 개요
이 프로젝트의 목표는 터미널, Docker, Git/GitHub를 활용하여 재현 가능한 개발 워크스테이션 환경을 구성하고, 그 과정을 문서로 정리하는 것이다. 터미널을 이용해 작업 디렉토리와 권한을 부여하고, Docker를 설치 및 점검한 뒤 컨테이너를 실행 및 관리한다. 또한 Dockerfile을 기반으로 간단한 웹 서버 이미지를 제작하고, 포트 매핑으로 접속을 확인하며 바인드 마운트와 볼륨을 사용해 변경 반영과 데이터 영속성을 확인한다.

### 2. 실행 환경
- OS: macOS
- Shell: bash
- Docker: 28.3.2
- Git: 2.45.2

### 3. 수행 항목 체크리스트
- [x] 터미널 기본 조작 및 폴더 구성
- [ ] 권한 변경 실습
- [ ] Docker 설치/점검
- [ ] hello-world 실행
- [ ] Dockerfile 빌드/실행
- [ ] 포트 매핑 접속(2회)
- [ ] 바인드 마운트 반영
- [ ] 볼륨 영속성
- [ ] Git 설정 + VSCode GitHub 연동

### 4. 터미널 조작 로그 기록

#### 1) 현재 위치 확인
현재 작업 중인 디렉토리의 절대 경로를 확인할 수 있음
```
➜  codyssey-m1 git:(main) pwd
/Users/kim-yejoo/Codyssey-2026/codyssey-m1
```

#### 2) 목록 확인(숨김 파일 포함)
현재 위치나 특정 디렉토리의 리스트를 출력
```
➜  codyssey-m1 git:(main) ✗ ls -alh
total 8
drwxr-xr-x   4 kim-yejoo  staff   128B Mar 31 17:24 .
drwxr-xr-x   3 kim-yejoo  staff    96B Mar 31 17:24 ..
drwxr-xr-x  13 kim-yejoo  staff   416B Apr  1 09:16 .git
-rw-r--r--   1 kim-yejoo  staff   1.5K Apr  1 09:26 README.md
```
```
➜  codyssey-m1 git:(main) ✗ ls -alh ../
total 0
drwxr-xr-x    3 kim-yejoo  staff    96B Mar 31 17:24 .
drwxr-x---+ 110 kim-yejoo  staff   3.4K Apr  1 10:18 ..
drwxr-xr-x    6 kim-yejoo  staff   192B Apr  1 09:41 codyssey-m1
```
옵션
- `-a`: all의 줄임말로, 숨김 파일 및 디렉토리를 포함한 모든 파일을 출력
- `-l`: long의 줄임말로, 파일 출력 형식을 긴 목록 형식으로 출력 (파일 타입, 권한, 소유자, 그룹, 파일 크기, 수정시간 등)
 - `-h`: human의 줄임말로, 사용자가 보기 좋은 형태의 단위로 출력
  
#### 3) 이동
현재 작업 중인 디렉토리 위치를 변경
```
➜  codyssey-m1 git:(main) ✗ pwd
/Users/kim-yejoo/Codyssey-2026/codyssey-m1
➜  codyssey-m1 git:(main) ✗ cd ..
➜  Codyssey-2026 git:(master) ✗ pwd
/Users/kim-yejoo/Codyssey-2026
```

#### 4) 디렉토리 생성
```
➜  codyssey-m1 git:(main) ✗ ls -a
.         ..        .git      README.md
➜  codyssey-m1 git:(main) ✗ mkdir test-dir
➜  codyssey-m1 git:(main) ✗ ls -a
.         ..        .git      README.md test-dir
```
```
➜  codyssey-m1 git:(main) ✗ ls
README.md test-dir  test.txt
➜  codyssey-m1 git:(main) ✗ mkdir ../codyssey-m1/text2-dir
➜  codyssey-m1 git:(main) ✗ ls
README.md test-dir  test.txt  text2-dir
```

#### 5) 파일 생성
```
➜  codyssey-m1 git:(main) ✗ ls -a 
.         ..        .git      README.md test-dir
➜  codyssey-m1 git:(main) ✗ touch test.txt
➜  codyssey-m1 git:(main) ✗ ls -a
.         ..        .git      README.md test-dir  test.txt
```

#### 6) 파일 내용 확인
```
➜  codyssey-m1 git:(main) ✗ cat test.txt 
➜  codyssey-m1 git:(main) ✗ 
```

#### 7) 파일에 내용 작성
```
➜  codyssey-m1 git:(main) ✗ cat test.txt 
➜  codyssey-m1 git:(main) ✗ echo "test file" > test.txt
➜  codyssey-m1 git:(main) ✗ cat test.txt
test file
```

#### 8) 파일 복사
```
➜  codyssey-m1 git:(main) ✗ ls
README.md test-dir  test.txt  text2-dir
➜  codyssey-m1 git:(main) ✗ cp test.txt copy.txt
➜  codyssey-m1 git:(main) ✗ ls
copy.txt  README.md test-dir  test.txt  text2-dir
➜  codyssey-m1 git:(main) ✗ cat copy.txt 
test file
```

#### 9) 디렉토리 복사
```
➜  Codyssey-2026 git:(master) ✗ cp -r codyssey-m1 copy-dir
➜  Codyssey-2026 git:(master) ✗ ls
codyssey-m1 copy-dir
➜  Codyssey-2026 git:(master) ✗ cd copy-dir 
➜  copy-dir git:(main) ✗ ls
copy.txt  README.md test-dir  test.txt  text2-dir
```

#### 10) 파일 이동
파일, 디렉토리 이동과 이름 변경 시 모두 `mv` 명령어 사용

파일 이동: `mv [파일명] [이동할 디렉토리 경로]`
```
➜  codyssey-m1 git:(main) ✗ touch moving.txt
➜  codyssey-m1 git:(main) ✗ mv moving.txt ../copy-dir 
➜  codyssey-m1 git:(main) ✗ ls
copy.txt  README.md test-dir  test.txt  text2-dir
➜  codyssey-m1 git:(main) ✗ cd ../copy-dir/ 
➜  copy-dir git:(main) ✗ ls
copy.txt   moving.txt README.md  test-dir   test.txt   text2-dir
```

#### 11) 파일 이름 변경
파일 이름 변경: `mv [기존 파일명] [새로운 파일명]`
```
➜  copy-dir git:(main) ✗ ls
copy.txt   moving.txt README.md  test-dir   test.txt   text2-dir
➜  copy-dir git:(main) ✗ mv moving.txt new.txt
➜  copy-dir git:(main) ✗ ls
copy.txt  new.txt   README.md test-dir  test.txt  text2-dir
```

#### 12) 디렉토리 이동
디렉토리 이동: `mv [디렉토리명] [목적지]`
```
➜  copy-dir git:(main) ✗ mkdir moving-dir
➜  copy-dir git:(main) ✗ mv moving-dir ../codyssey-m1 
➜  copy-dir git:(main) ✗ cd ../codyssey-m1 
➜  codyssey-m1 git:(main) ✗ ls
copy.txt   moving-dir README.md  test-dir   test.txt   text2-dir
```

#### 13) 디렉토리 이름 변경
디렉토리 이름 변경: `mv [기존 디렉토리명] [새로운 디렉토리명]`
```
➜  codyssey-m1 git:(main) ✗ ls
copy.txt   moving-dir README.md  test-dir   test.txt   text2-dir
➜  codyssey-m1 git:(main) ✗ mv moving-dir new-dir
➜  codyssey-m1 git:(main) ✗ ls
copy.txt  new-dir   README.md test-dir  test.txt  text2-dir
```

#### 14) 파일 삭제
```
➜  codyssey-m1 git:(main) ✗ ls
copy.txt  new-dir   README.md test-dir  test.txt  text2-dir
➜  codyssey-m1 git:(main) ✗ rm test.txt copy.txt 
➜  codyssey-m1 git:(main) ✗ ls
new-dir   README.md test-dir  text2-dir
```

#### 15) 디렉토리 삭제
빈 디렉토리 삭제: `rmdir [디렉토리명]`, `rm -d [디렉토리명]`
```
➜  codyssey-m1 git:(main) ✗ ls
new-dir   README.md test-dir  text2-dir
➜  codyssey-m1 git:(main) ✗ rmdir new-dir
➜  codyssey-m1 git:(main) ✗ rm -d test-dir text2-dir
➜  codyssey-m1 git:(main) ✗ ls
README.md
```
디렉토리 및 전체 내용 삭제: `rm -r [디렉토리명]`, `rm -rf [디렉토리명]`
```
➜  Codyssey-2026 git:(master) ✗ ls
codyssey-m1 copy-dir
➜  Codyssey-2026 git:(master) ✗ rm -rf copy-dir 
➜  Codyssey-2026 git:(master) ✗ ls
codyssey-m1
```
### 5. 권한 실습 및 로그 기록

### 6. Docker 설치 및 기본 점검

### 7. Docker 기본 운영 명령 수행

### 8. 컨테이너 실행 실습

### 9. 기존 Dockerfile 기반 커스텀 이미지 제작

### 10. 포트 매핑 및 접속 증거

### 11. Docker 볼륨 영속성 검증

### 12. Git 설정 및 GitHub 연동
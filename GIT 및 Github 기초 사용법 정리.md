# GIT 및 Github 기초 사용법 정리

등록 2024.6.13

---

## 1. 개요

Git

- 파일의 수정 사항을 저장하고 관리하는 버전 컨트롤 시스템 (VCS, Virsion Control System)

Github

- Git으로 관리하는 파일을 업로드하거나 다운로드 할 수 있는 웹 인터페이스.
- 본인의 작업물을 공유하거나, 여러 사람과 협업 하는 등 용도로 쓰인다.

## 2. 사전지식

1. commit: 파일을 추가하거나 변경 내용을 저장소에 저장하는 작업
2. push: 커밋 내용을 원격 저장소(깃허브 레포지터리)에 업로드
3. pull: 원격저장소의 파일을 내 로컬 저장소에 저장
4. branch: 하나의 레포지터리에 나누어 놓은 여러 개별 공간. 각각의 브랜치는 다른 브랜치에 영향을 주지 않음.
5. merge: 다른 브랜치의 내용을 하나의 브랜치에 병합하는 과정. 주로 master라는 이름의 브랜치에 병합.

<aside>
💡 브랜치(Branch)

브랜치는 로컬저장소(본인 컴퓨터 Git)와 원격저장소(Github 레포지터리)에서 각각 존재한다. 다시 말해, 본인 컴퓨터 Git에서 생성한 branch와 Github에 생성된 branch는 별개이다.

디폴트 브랜치 이름은 일반적으로 master이지만 최근 이 표현이 과거 노예제도를 연상시킨다는 이슈가 있어 main으로 바꾸는 추세이다. 디폴트 브랜치 이름은 깃허브에서 변경 가능하다.

</aside>

## 3. Git 및 Github 사용 준비

### 1) 깃허브 계정 생성

[https://github.com/](https://github.com/)

### 2) 깃 설치

[https://git-scm.com/](https://git-scm.com/) 

### 3) 깃 초기 설정

- 사용자 등록

```powershell
git config --global user.name "[사용자 이름]" 
git config --global user.email [사용자 메일]
```

- 설정 정보 확인

```powershell
git config --list 
```

## 4. 기본적인 push, pull 하는 법

### 1) 깃허브 레포지터리 생성

깃허브 홈페이지 repository 탭에서 만들 수 있다.

### 2) 로컬 저장소에 깃 저장소 생성 및 원격 저장소 연결

- 깃 저장소 생성(깃 초기화)

해당 로컬 저장소(디렉토리)로 이동 후 아래 명령어를 입력

```powershell
git init
```

- 원격 저장소 연결(remote)

```powershell
git remote add origin [깃허브 레포지터리 URL]
```

### 3) Push

- 스테이지(커밋할 파일을 추가하는 작업)

```powershell
git add [파일명]
```

파일명에는 *과 같은 정규표현식 사용이 가능하다.

- 커밋

```powershell
git commit -m "[커밋 메세지 입력]" 
```

- 현재 깃 커밋, 스테이지 상태 확인

```powershell
git status
```

- 푸시(push)

```powershell
git push origin master 
```

이후, 깃허브에 접속하면 해당 파일이 master 브랜치에 업로드 되어있는 것을 확인할 수 있다. 

### 4) Pull

```powershell
git pull origin master 
```

이후, 로컬 저장소를 확인해 보면 원격 저장소의 파일이 다운로드 되어있는 것을 확인할 수 있다.

## 5. 여러 브랜치를 만들고 협업하기

### 1) 협업할 때 사용할 깃허브 레포지터리 만들기

깃허브에서 협업하기 위한 레포지터리들을 모아 놓는 조직(Organization)을 만들 수도 있다. 또한 조직과 레포지터리에서 각 사용자의 권한설정 및 외부 공개 여부도 설정 가능하다.

### 2) 공동 작업자 추가

깃허브에서 팀원의 깃허브 이메일 주소를 활용해 등록할 수 있다. 발송된 이메일을 각 팀원이 확인하고 수락을 누르면 추가되는 방식.

### 3) 공동 작업자의 PC 로컬 저장소에 원격 저장소 연결(clone)

공동 작업자 스스로 작업물을 저장할 로컬 저장소 경로로 이동하여 아래 명령어를 입력한다.

```powershell
git clone [레포지터리 URL]
```

<aside>
💡 remote와 clone의 차이

git remote add 명령어는 원격 저장소를 로컬 깃 프로젝트에 추가하는 것을 의미한다. 이 명령을 사용함으로써 로컬 깃 프로젝트와 원격 저장소 간의 연결이 설정된다. 즉, 로컬에서 작업한 변경사항을 원격 저장소로 업로드하거나, 원격 저장소에서 최신 변경사항을 로컬로 내려받을 때 사용된다. 따라서 이 명령어를 사용하려면 이미 로컬 저장소에 git이 생성되어 있어야 한다.

반면에, git clone 명령어는 원격 저장소의 전체 내용을 복제하여 로컬에 새로운 깃 프로젝트를 생성하는 것을 의미한다. 이 명령을 사용하면 원격 저장소의 모든 파일과 히스토리, 브랜치 등을 로컬로 가져올 수 있다. 

결론적으로, 레포지터리 관리자는 깃 프로젝트를 만들어 레포지터리에 remote하고, 공동 작업자는 관리자가 만든 레포지터리를 clone하여 협업한다.

</aside>

### 4) 공동 작업자 브랜치 생성하기

- 브랜치 생성

```powershell
git branch [브랜치 이름]
```

- 해당 브랜치로 이동

```powershell
git checkout [브랜치 이름]
```

- 브랜치 생성과 동시에 해당 브랜치로 이동하는 명령어

```powershell
git checkout -b [브랜치 이름]
```

- 로컬 브랜치를 원격 브랜치에 푸시하기

```powershell
git push origin [브랜치 이름]
```

- 로컬 브랜치와 원격 브랜치 연동하기

```powershell
 # 필수적인 명령은 아니다.
 # 생성된 브랜치는 로컬과 원격에 각각 따로 존재하므로, 이를 연동시켜 편리하게 작업하는 방법
 git branch --set-upstream-to origin/[브랜치 이름]
```

### 5) 브랜치 확인 및 삭제 명령어

- 로컬 브랜치 확인

```powershell
git branch
```

- 원격 브랜치 확인

```powershell
git branch -r
```

- 모든 브랜치 확인

```powershell
git branch -a
```

브랜치 확인 명령어 입력시 앞에 *이 붙어 있는 것은 현재 브랜치라는 뜻이다.

- 로컬 브랜치 삭제

다른 브랜치로 체크아웃 후 아래 명령어를 입력

```powershell
git branch -d [브랜치 이름]
```

- 로컬 브랜치 강제 삭제

해당 로컬 브랜치에 완료되지 않은 작업이 남아있어 삭제가 되지 않는 경우 사용한다. 

역시 다른 브랜치로 체크아웃 후 아래 명령어를 입력한다.

```powershell
git branch -D [브랜치 이름]
```

### 6) 브랜치에 push 하기

<aside>
💡 협업 시 주의 사항!

공동 작업하는 과정에서 브랜치의 파일 내용이 변경되었을 수 있으니, 파일 수정 작업 및 push 하기 전 항상 pull을 먼저 해야 한다.

</aside>

- 해당 브랜치로 체크아웃

(생략)

- 스테이징

(생략)

- 커밋

(생략)

- 푸시

```powershell
 git push origin [브랜치 이름]
```

위와 같이 로컬 브랜치를 생성하고 원격 레포지터리에 푸시하면 해당 로컬 브랜치가 자동으로 원격 브랜치로 추가된다.

이후 깃허브에서 해당 브랜치가 생성되고 그 브랜치에 파일이 업로드 된 것을 확인할 수 있다.

## 6. 병합하기

### 1) 로컬 브랜치에 병합하기

- 병합하고자 하는 브랜치로 체크아웃(디폴트 브랜치, 주로 master)

(생략)

- 브랜치 병합

```powershell
git merge [병합할 브랜치 이름] 
```

이후 로컬 디폴트 브랜치(master)에 해당 브랜치 내용이 병합된다.

### 2) 원격 저장소(깃허브 레포지터리)에 병합하기

로컬 브랜치에서 병합하는 것 보단 깃허브 레포지터리의 디폴트 브랜치에 병합하는 작업을 더 많이 수행한다.

깃허브는 pull request라고 하여, 개별 브랜치 내용을 디폴트 브랜치에 병합하는 요청을 보내는 기능이 있다. 아래는 pull request를 활용하여 깃허브에서 병합하는 방법을 기술한 내용이다.

- 공동 작업자가 자신의 브랜치에 결과물을 push

(생략)

- 공동 작업자가 깃허브 웹에서 pull request를 클릭하여 요청 생성
- 관리자는 확인 후 merge pull request를 클릭해 병합

이후 디폴트 브랜치에 공동 작업자의 브랜치 내용이 병합된 것을 확인할 수 있다.

## 7. 기타 유용한 기능

### 1) CRLF 설정

깃 push, pull 할 때 자동으로 CR과 LF를 변환해주는 기능

- 해당 깃에만 설정

```powershell
git config core.autocrlf true
```

- 전역설정

```powershell
git config --global core.autocrlf true
```

해제 시에는 위 명령어에서 true 대신 false를 사용하면 된다.

위 명령어는 윈도우 전용 명령이다.

### 2) 강제 push, pull

<aside>
💡 병합충돌(merge conflicts)

merge시 변경 내용을 자동으로 병합해주지 못해 발생하는 오류를 병합충돌(merge conflicts)라고 한다. 

병합 충돌 발생 시, 깃허브 pull request로 병합할 때 직접 충돌 부분을 수정하고 병합할 수 있다.

</aside>

아래는 병합 충돌을 무시하고 강제로 push, pull 하고 싶을 때 쓰는 명령어이다.

- 강제 push

```powershell
git push origin [push 하고자 하는 브랜치 이름] --force

# 예를들어 master 브랜치에 강제 push 할 때
git push origin master --force
```

- 강제 pull

```powershell
git fetch --all
git reset --hard origin/[pull 하고자 하는 브랜치 이름]
git pull origin [pull 하고자 하는 브랜치 이름]

# 예를들어 master 브랜치에 강제 pull 할 때
git fetch --all
git reset --hard origin/master
git pull origin master
```

### 3) pull request에서 병합 충돌 해결하기

pull request시 병합충돌이 발생하면 깃허브에서 이를 해결하는 인터페이스를 제공해준다.

- pull request시 병합충돌이 발생하면 reseolve conflicts 버튼을 클릭한다.
- resoleve conflicts에 진입하면 소스코드에 아래 기호가 표시된다.

```powershell
If you have questions, please
<<<<<<< HEAD
open an issue
=======
ask your question in IRC.
>>>>>>> [병합하는 브랜치 이름]
```

여기서 <<<<<<< HEAD 부터 =======까지는 기존 내용,

======= 부터 >>>>>>>까지는 병합하는 브랜치에서 변경된 내용이다.

- 소스코드를 직접 수정하고 <<<<<<<과 =======을 지운다.
- mark as resolved 버튼을 클릭하여 병합 충돌을 해결한다.

## 8. 추가로 알아볼 것

1. fork
2. fetch와 pull 차이점
3. diff
4. HEAD와 FETCH_HEAD
5. origin과 upstream, downstream
6. 기타 위에서 소개한 명령어의 여러 옵션들
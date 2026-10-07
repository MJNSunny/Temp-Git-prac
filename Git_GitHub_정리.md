# Git & GitHub 정리

> 과정 목표: Git과 GitHub를 활용해 코드를 안전하게 관리하고 협업할 수 있는 기본 역량을 갖춘다.

## 목차

1. 버전 관리의 필요성
2. Git 기본 개념
3. Git 설치와 초기 설정
4. 로컬에서 Git 사용하기
5. 브랜치 이해하기
6. GitHub 기초
7. 협업 실습
8. 자주 사용하는 명령어

---

## 1. 버전 관리의 필요성

### 버전 관리(Version Control)란?

- 파일이나 코드의 변경 이력을 체계적으로 기록하고 관리하는 것
- 언제, 누가, 무엇을 바꿨는지 알 수 있고, 필요하면 과거 상태로 되돌릴 수 있음

### 왜 필요한가?

- 변경 이력을 추적하고, 실수를 복구하며, 여러 사람이 충돌 없이 협업하기 위해
- 기능 추가 중 버그가 생겼을 때 이전 정상 동작 버전으로 바로 되돌릴 수 있다
- 팀원이 동시에 같은 파일을 수정해도 누가 무엇을 바꿨는지 확인하고 충돌을 해결할 수 있다
- "최종_진짜최종_v3" 같은 파일을 만들지 않고도 변경 과정을 깔끔하게 관리할 수 있다

### Git vs. 파일 복사

| 구분 | 파일 복사 방식 | Git 사용 |
|---|---|---|
| 방식 | `final.py`, `final_v2.py`, `진짜최종.py`처럼 파일이 늘어남 | 변경 내용이 **커밋** 단위로 기록됨 |
| 이력 | 변경 이유와 내용이 남지 않음 | 언제든 특정 시점으로 되돌릴 수 있음 |
| 협업 | 어떤 파일이 최신인지 알기 어려움 | 여러 사람이 동시에 작업 가능, 변경 이력과 책임이 명확 |

### Git vs. GitHub

| | Git | GitHub |
|---|---|---|
| 정체 | 버전 관리를 위한 도구(프로그램) | Git 저장소를 올려두는 웹 서비스 |
| 위치 | 내 컴퓨터에서 동작 | 코드 공유 및 협업 플랫폼 |
| 기능 | 버전 관리 | Pull Request, Issue, Review 기능 제공 |

**Git은 버전 관리 엔진, GitHub는 협업과 공유를 위한 서비스**

---

## 2. Git 기본 개념

### Repository (레포지토리)

- 파일과 그 변경 이력을 함께 관리하는 저장소. 프로젝트 전체와 모든 버전 기록이 들어 있음
- **로컬 저장소**: 내 컴퓨터에 있는 저장소
  - 프로젝트 폴더로 이동 → `git init` 실행 → 해당 폴더가 Git 레포지토리가 됨
- **원격 저장소**: GitHub 같은 서버에 있는 저장소
  - GitHub에서 새 Repository 생성 → `git clone`으로 내 컴퓨터에 복사

### Commit (커밋)

- 변경 사항을 하나의 기록으로 저장하는 단위 (= 하나의 버전)
- "무엇을 왜 바꿨는지"를 메시지로 남김
- 특정 시점의 프로젝트 상태를 저장, 되돌아갈 수 있는 기준점 역할
- 생성: `git commit -m "회원가입 기능 추가"`

### Branch (브랜치)

- 독립적으로 작업할 수 있는 작업 공간
- 기존 코드를 건드리지 않고 기능 개발 가능, 여러 기능을 동시에 개발 가능
- 작업이 끝나면 병합(merge)함
- 생성: `git branch feature/login` / 전환: `git switch feature/login`

### HEAD (헤드)

- 현재 내가 작업 중인 위치를 가리키는 포인터
- 보통 현재 브랜치의 최신 커밋을 가리킴
- HEAD가 움직인다는 것은 작업 기준이 바뀐다는 의미

```
version 1 → version 2 → version 3
                           ↑ HEAD
```

### Working Directory → Staging Area → Repository

```
working directory  --git add-->  staging area  --git commit-->  repository
```

- **Working Directory**: 실제로 파일을 수정하고 작업하는 공간. 아직 Git에 기록되지 않은 변경 사항이 있는 상태
- **Staging Area**: 다음 커밋에 포함할 변경 사항을 미리 모아두는 공간
  - Working Directory에서 Staging Area로 가는 법: `git add 파일명`

---

## 3. Git 설치와 초기 설정

### Git 설치

- macOS: `brew install git`
  - Homebrew: https://brew.sh/
- Windows: Git for Windows 설치 (Git for Windows/x64 Setup)
- 설치 확인: `git --version`

### GitHub 회원가입

- https://github.com/ 접속해서 회원가입 (name, email 기록)

### git config

Git의 기본 동작을 설정하는 명령어

```bash
# 전역 설정: 모든 저장소에 적용
git config --global user.name "홍길동"
git config --global user.email "hong@example.com"

# 로컬 설정: 특정 저장소에만 적용
# (프로젝트마다 다른 계정이나 역할을 써야 할 때 사용 - 회사 프로젝트와 개인 프로젝트 구분)
git config user.name "홍길동"
git config user.email "hong@example.com"
```

---

## 4. 로컬에서 Git 사용하기

| 명령어 | 설명 |
|---|---|
| `git init` | 현재 폴더를 Git 레포지토리로 초기화. `.git` 폴더가 생성되고, 현재 폴더를 기준으로 버전 관리 시작 |
| `git status` | 현재 레포지토리 상태 확인 (수정된 파일, 스테이징 여부, 커밋 가능한 변경 사항) |
| `git add 파일명` / `git add .` | 변경된 파일을 Staging Area로 올림. 커밋에 포함할 변경 사항을 선택하는 단계이며, 아직 커밋이 생성된 것은 아님 |
| `git commit -m "메시지"` | Staging Area의 변경 사항을 하나의 버전으로 기록. 되돌릴 수 있는 기준점 역할 |
| `git log` | 커밋 이력 확인 |

### 기본 흐름 예시

```bash
git init
git status
git add first.txt
git commit -m "first commit"
git log
```

### 커밋 메시지 작성 규칙

좋은 커밋 메시지는 무엇을 했는지 한눈에 알 수 있어야 한다.

- 명확하고 간결하게 작성
- 동사로 시작
- 한 커밋 = 한 작업
- 예시
  - `Add login API`
  - `Fix password validation bug`
  - `Refactor user service`

### .gitignore

버전 관리에서 제외할 파일을 지정하는 설정 파일

- 불필요한 파일이 커밋되는 것을 방지
- 환경 변수 파일, 빌드 결과물, 개인 설정 파일 등은 보통 제외
- 예시: `.env`, `__pycache__/`, `*.log`
- **주의**: 이미 커밋된 파일은 Git이 계속 추적하기 때문에 `git rm --cached 파일명` 필요

### 퀴즈 정리

| 문제 | 정답 |
|---|---|
| Git에서 하나의 작업 단위를 기록한 것은? | **C. commit** |
| Git을 사용하는 가장 큰 목적은? | **D. 코드 변경 이력을 관리하기 위해** |
| Working Directory와 Staging Area의 차이를 가장 잘 설명한 것은? | **B. 스테이징은 커밋할 파일을 선별하는 공간이다** |

> 임시백업은 애매함 → Git은 **원격이 아닌 로컬**, **자동이 아닌 수동** 방식이기 때문

---

## 5. 브랜치 이해하기

### Branch 주요 명령어

```bash
git branch                  # 브랜치 목록 확인
git branch feature/ui       # 브랜치 생성
git switch feature/ui       # 브랜치 전환
git switch -c feature/ui    # 생성과 동시에 전환
```

- 기존 작업과 분리된 독립적인 작업 흐름
- 기능 개발, 실험, 수정 작업을 안전하게 진행할 수 있음
- 협업과 안정적인 배포를 위해서는 브랜치를 잘 관리하는 것이 중요

### 브랜치 관리 전략

어떻게 브랜치를 나누고 합칠지에 대한 약속

- `main`: 배포 가능한 안정 버전
- `dev`: 개발 중인 기능을 테스트하는 버전
- `feature/*`: 기능 개발
- `hotfix/*`: 긴급 수정

### 브랜치 병합 (git merge)

다른 브랜치의 작업 내용을 **현재 브랜치로** 합치는 명령어

```bash
git switch main
git merge feature/ui
```

### Fast-forward vs. 3-way merge

| 구분 | Fast-forward merge | 3-way merge |
|---|---|---|
| 상황 | 브랜치가 직선으로 이어질 때 | 브랜치가 갈라졌다가 다시 합쳐질 때 |
| 동작 | 단순히 커밋 포인터만 이동 | 병합 커밋이 생성됨 |

**분기가 없으면 Fast-forward, 분기가 있으면 3-way merge**

```
Fast-forward:  main이 feature 위치로 그냥 이동
3-way merge:   main에도 새 커밋(2)이 있고 feature에도 커밋(1)이 있음 → 병합 커밋(3) 생성
```

#### 실습 메모

- Fast-forward 시 feature 브랜치(예: commit 5)의 변경 사항만 받아들여 main이 앞으로 이동
- 3-way merge 시 병합 커밋(merge commit) 메시지를 입력하는 에디터가 열림 → vim이라면 `:wq`로 저장 후 종료
- 병합 이력 보기: `git log --all --graph`

### Merge Conflict 해결

같은 파일의 같은 부분을 서로 다르게 수정하면 충돌 발생

**해결 방법**
1. 충돌 파일 확인
2. 충돌 코드 직접 수정
3. 새로운 커밋 생성

Git은 자동 병합을 시도하고, 판단이 필요한 경우만 충돌을 알려줌

> Git이 선택을 못 하기 때문에 **사람이 직접** 결정해야 함. 때로는 left/right 어느 쪽도 아닌 완전히 새로운 코드를 쓰기도 함.

### Merge Conflict 해결 실습

```bash
# Git 레포지토리 초기화
git init
echo "hello" > test.txt
git add .
git commit -m "first commit"

# feature 브랜치 생성 후 같은 파일 수정
git branch feature
git switch feature
echo "hello from feature" > test.txt
git add .
git commit -m "update from feature"

# main에서 다시 수정
git switch main
echo "hello from main" > test.txt
git commit -am "update from main"

# 병합 → 충돌 발생
git merge feature
```

충돌 후 흐름: `git merge` → **CONFLICT!!** → 충돌 코드 수정 → `git add` → `git commit` (병합 완료)

```
feature:           hello from feature
main:   hello  →   hello from main     →  ❓ (어느 쪽을 선택?)
```

#### 실습 메모

- 같은 파일을 두 개의 브랜치(left, right)에서 수정한 뒤 `git merge left` / `git merge right`
- 브랜치를 병합한 뒤 필요 없어진 브랜치는 Git이 알아서 지워주지 않으므로 직접 삭제해야 함 (main 브랜치만 남기고 삭제)

---

## 6. GitHub 기초

### GitHub 계정과 저장소 생성

- Git 저장소를 호스팅하는 서비스
- 계정을 만든 뒤 새 Repository를 생성하면 원격 저장소 주소(URL)가 발급됨

**원격 저장소**
- 인터넷에 있는 Git 저장소
- 여러 사람이 같은 코드 공유, 백업 역할, 협업의 기준점

```bash
git remote add origin 원격주소
git remote -v
```

### git push / git pull

로컬과 원격 저장소를 동기화하는 명령어

- `git push`: 로컬 커밋을 원격 저장소로 올림
- `git pull`: 원격 변경 사항을 내려받아 로컬에 반영

```bash
# 1. 로컬 커밋을 원격 저장소로 업로드
git push -u origin main

# 2. GitHub 웹에서 파일 추가 및 커밋 생성

# 3. 원격 저장소의 변경 사항 다운로드
git pull
```

---

## 7. 협업 실습

### Clone vs. Fork

| | Clone | Fork |
|---|---|---|
| 의미 | 원격 저장소를 그대로 내 로컬로 복사 | 다른 사람의 저장소를 내 GitHub 계정으로 복사 |
| 사용 시점 | 같은 저장소에 push 권한이 있을 때 | 원본 저장소에 직접 push 권한이 없을 때 |
| 용도 | 팀 내부 협업에 주로 사용 | 오픈소스 기여 방식 |

### Pull Request (PR)

변경 사항을 원본 저장소에 반영해달라고 요청하는 것

- 변경 내용 설명
- 리뷰 요청
- 병합 전 검증 단계

### Code Review 기본

코드를 병합하기 전에 함께 확인하는 과정

- 목적: 버그 예방, 코드 품질 유지, 팀 규칙 공유
- 기본 원칙: 코드 중심으로 리뷰 / 이유를 남긴 코멘트 / 승인 후 병합

### Issue 사용법

할 일, 버그 리포트, 기능 요청 등을 관리하는 기능 → PR과 Issue를 연결하여 작업 관리

- 예시: `Resolve: #1234`

### 협업 실습 (Fork & Clone)

1. Issue 생성
2. 내 GitHub 계정으로 Fork
3. Clone으로 코드 가져오기
   - `git clone 내_포크_저장소_URL`
4. 원본 저장소 연결
   - `git remote add upstream 원본_저장소_URL`
5. 최신 코드 받기
   - `git pull upstream main`
6. 브랜치 생성
   - `git switch -c feature/add-my-name`

### 협업 실습 (Collaborator)

1. Repository collaborator 등록
2. Branch protection rules 추가
   - Require a pull request before merging
3. Clone으로 코드 가져오기
   - `git clone 원본_저장소_URL`
4. 새로운 브랜치 생성 & 커밋
   - `git switch -c feature/mybranch` & `git commit -m "message"`
5. 원격 브랜치에 push
   - `git push origin feature/mybranch`
6. Pull Request 생성
   - GitHub에서 `feature/mybranch` → `main` PR 생성

---

## 8. 자주 사용하는 명령어

### git show

특정 커밋 하나를 집중해서 살펴볼 때 사용

- 해당 커밋의 변경 내용(diff), 커밋 메시지·작성자·날짜 출력
- 코드 리뷰나 이력 확인 시 사용

| 명령어 | 설명 |
|---|---|
| `git show` | `git show HEAD`와 동일 |
| `git show HEAD` | 현재 브랜치의 최신 커밋 내용 확인 |
| `git show 커밋해시` | 특정 커밋 하나를 지정해서 확인 |

### git diff

두 상태 간의 차이점만 비교해서 보여주는 명령어 (커밋 전 변경 사항 점검, 병합·충돌 원인 분석)

| 명령어 | 비교 대상 |
|---|---|
| `git diff` | Working Directory ↔ Staging Area |
| `git diff --staged` | Staging Area ↔ HEAD |
| `git diff HEAD~1 HEAD` | 커밋 ↔ 커밋 |

### git blame

파일의 각 줄이 누가, 언제, 어떤 커밋에서 수정됐는지 추적 (버그 원인 추적 시, "이 줄은 왜 이렇게 되어 있지?")

```bash
git blame main.py
```

### git stash

현재 작업 중인 변경 사항을 임시로 치워두는 명령어 (커밋하지 않고 작업을 잠시 중단, 브랜치 이동이나 긴급 수정 시 유용)

| 명령어 | 설명 |
|---|---|
| `git stash` | 현재 작업 중인 변경 사항을 임시로 저장 |
| `git stash list` | 지금까지 저장된 stash 목록 확인 |
| `git stash pop` | 가장 최근에 저장한 stash를 다시 적용하고 목록에서 제거 |
| `git stash apply` | 특정 stash를 제거하지 않고 적용만 하려면 |

### git reset

브랜치의 기준을 과거 커밋으로 이동시키는 명령어 (**히스토리를 바꿈**)

- `--soft`: 커밋만 취소 (변경 내용 유지)
- `--mixed` (기본): 커밋 + 스테이징 취소
- `--hard`: 전부 삭제 (**주의**)
- 협업 브랜치에서 사용 시 주의

| 명령어 | 설명 |
|---|---|
| `git reset --soft HEAD~1` | HEAD만 한 커밋 이전으로 이동 (변경 내용은 유지) |
| `git reset --hard HEAD~1` | HEAD 이동 + 스테이징 + 파일까지 모두 되돌림 |

### git revert

특정 커밋을 되돌리는 **새 커밋**을 생성 (히스토리를 보존)

- 기존 기록은 그대로 유지
- "이 커밋을 취소했다"는 기록이 남음
- 협업 중 안전하게 롤백할 때 사용

```bash
git revert 커밋해시
```

### git commit --amend

마지막 커밋을 고치는 옵션

- 가장 최근 커밋을 새 커밋으로 교체
- 커밋 메시지 수정 가능
- 변경 파일 추가/제거 가능

| 명령어 | 설명 |
|---|---|
| `git commit --amend` | 마지막 커밋을 고친다 |
| `git commit --amend --no-edit` | 기존 커밋 메시지는 그대로 유지 |

---

## 한눈에 보는 명령어 치트시트

| 목적 | 명령어 |
|---|---|
| 저장소 초기화 | `git init` |
| 원격 저장소 복사 | `git clone URL` |
| 상태 확인 | `git status` |
| 스테이징 | `git add 파일명` / `git add .` |
| 커밋 | `git commit -m "메시지"` |
| 이력 확인 | `git log`, `git log --all --graph` |
| 브랜치 목록/생성/전환 | `git branch` / `git branch 이름` / `git switch 이름` |
| 브랜치 생성 + 전환 | `git switch -c 이름` |
| 병합 | `git merge 브랜치명` |
| 원격 연결 | `git remote add origin URL` |
| 업로드 / 다운로드 | `git push` / `git pull` |
| 변경 비교 | `git diff` |
| 커밋 상세 | `git show` |
| 줄별 작성자 추적 | `git blame 파일명` |
| 임시 저장 | `git stash` / `git stash pop` |
| 커밋 취소 (이력 변경) | `git reset` |
| 커밋 취소 (이력 보존) | `git revert` |
| 마지막 커밋 수정 | `git commit --amend` |

---

## 개인 필기 / 주의할 점

- Mac에서는 Homebrew(https://brew.sh/)로 설치. Windows는 PowerShell 사용
- VS Code에서 Git Bash 셸 커맨드(`Ctrl+Shift+P`)로 코드를 불러오는 설정은 아직 못 함 / Autosave도 설정 못 함
- `git log`에서 이력이 덮어써진 것처럼 보였지만, 화면 아래에 이어서 있었음 → **아래쪽 화살표**로 스크롤하면 됨 (종료는 `q`)
- `.gitignore`가 어떻게 동작하는지, ID/PW가 있던 `.env` 파일이 어디 갔는지 다시 확인해보기 (`.gitignore`에 `.env` 추가하면 추적 대상에서 제외됨, 파일 자체는 삭제되지 않음)
- Fast-forward는 5번 커밋의 변경 사항만 받아들이고 포인터만 이동한 것
- 3-way merge 이후 `git log --all --graph`로 보면 병합 커밋과 양쪽 브랜치 이력이 모두 보임
- Conflict는 같은 위치를 다르게 수정했을 때 발생. Git이 선택을 못 하므로 사람이 해결
- 브랜치 삭제는 Git이 알아서 해주지 않음. 병합 후 직접 정리 (`git branch -d 브랜치명`)

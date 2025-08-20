# ✅ 1단계) Git 기본 세팅 (CLI)

이 단계는 **Git을 쓸 때 꼭 필요한 최소한의 설정**과 **프로젝트 초기 세팅**을 하는 과정입니다.

---

## 1-1. 사용자 정보 설정 (최초 1회만 하면 됨)

```bash
git config --global user.name  "Seung Il Baek"      # 본인 이름/닉네임
git config --global user.email "you@example.com"   # GitHub 이메일
```

* 커밋할 때 "누가 작업했는지" 표시되는 정보입니다.
* `--global` 옵션은 PC 전체 공통 설정이라, 다른 프로젝트에서도 동일하게 적용됩니다.

👉 확인:

```bash
git config --global -l
```

---

## 1-2. 브랜치 기본 이름을 main 으로 통일

```bash
git config --global init.defaultBranch main
```

* 요즘은 기본 브랜치명을 `master` 대신 `main`으로 쓰는 것이 표준입니다.

---

## 1-3. 라인 엔딩(Windows ↔ Linux 호환)

```bash
git config --global core.autocrlf true
git config --global core.safecrlf warn
```

* Windows에서는 엔딩이 CRLF, Linux는 LF라서 충돌 방지용입니다.

---

## 1-4. 자격 증명 저장 (로그인 편하게)

```bash
git config --global credential.helper manager
```

* GitHub에 push할 때 매번 비밀번호 입력할 필요 없이 Windows Credential Manager에 저장됩니다.

---

## 1-5. Git 저장소 초기화 (GitTest 프로젝트 폴더에서 실행)

```bash
cd D:/TOYPROJECT/GitTest   # 프로젝트 폴더로 이동
git init
```

* `.git` 폴더가 생기고, 여기가 이제 Git 저장소가 됩니다.

---

## 1-6. 불필요한 파일 제외 설정 (.gitignore)

### 파일 만들기

GitTest 루트 폴더에서 Git Bash 실행 후:

```bash
touch .gitignore
notepad .gitignore
```

메모장에서 아래 내용을 붙여넣고 저장합니다.

```gitignore
# Visual Studio / WinForms build 산출물 제외
[Bb]in/
[Oo]bj/
.vs/
*.user
*.suo
*.userosscache
*.sln.docstates

# NuGet 패키지
packages/
*.nupkg

# 로그/캐시
*.log
*.cache
*.pdb
*.db

# OS 관련
Thumbs.db
.DS_Store
```

### 정상 동작 확인

```bash
git check-ignore -v bin/Debug/*
```

출력 예시:

```
.gitignore:2:[Bb]in/    bin/Debug/*
```

→ `.gitignore` 가 정상적으로 적용된 상태.

---

## 1-7. 초기 스냅샷(첫 커밋)

```bash
git add .
git commit -m "chore: initial commit (WinForms .NET Framework 4.8.1 - GitTest)"
```

* 현재 프로젝트 전체를 첫 버전으로 기록합니다.

---

## 1-8. GitHub 원격 저장소 연결

### HTTPS 방식

```bash
git remote add origin https://github.com/<YOUR_ID>/<Repo>.git
git push -u origin main
```

* `<YOUR_ID>` = GitHub 사용자명 (예: Seung0224)
* `<Repo>` = GitHub에서 만든 저장소 이름 (예: GitTest-VisualStudio2022)

### SSH 방식

```bash
git remote add origin git@github.com:<YOUR_ID>/<Repo>.git
git push -u origin main
```

* 사전에 GitHub에 SSH Key 등록 필요

---

## 📌 깔끔하게 push 하려면: GitHub 리포 만들기 베스트 프랙티스

### 방법 1) 로컬 우선(Local-first) ― 추천

* GitHub에서 새 리포 생성할 때 **빈 저장소(Empty)** 로 만든다.
  (❌ Add a README, ❌ Add .gitignore, ❌ Add license)
* 로컬에서 commit → push

```bash
git init
git add .
git commit -m "chore: initial commit"
git remote add origin https://github.com/<ID>/<Repo>.git
git push -u origin main
```

### 방법 2) GitHub 우선(Remote-first)

* GitHub에서 리포 생성 시 ✅ README / .gitignore / License 체크 (초기 커밋 생성)
* 로컬은 반드시 `git clone` 으로 시작해야 한다.

```bash
git clone https://github.com/<ID>/<Repo>.git
cd <Repo>
# 작업 후
git add .
git commit -m "feat: ..."
git push
```

### 피해야 할 패턴 (에러 원인)

* GitHub에서 README로 초기화된 리포를 만든 뒤,
* 로컬에서는 이미 `git init` 한 폴더에서

```bash
git remote add origin ...
git push -u origin main
```

→ ❌ `fetch first`, `unrelated histories` 오류 발생

---

# 🎉 완료

* PC 전역 Git 환경 설정 완료
* `.gitignore` 적용 완료
* `GitTest` 프로젝트가 Git으로 관리 시작
* (선택) GitHub 원격 저장소와 동기화 완료

---

# ▶️ 2단계) WinForms에 버튼 3개 추가 → 각 단계 커밋 → "시간여행" 실습

(여기에 2단계 진행하면서 커밋 스냅샷과 명령어를 추가해 나갑니다.)

---

# ▶️ 3단계) 선택적 반영: 1번/3번 버튼만 포함하고 2번은 제외 (Cherry-pick)

(여기에 체리픽 시나리오와 명령어를 추가해 나갑니다.)

---

# ▶️ 4단계) SourceTree로 동일 작업 해보기 (GUI)

(여기에 SourceTree 설치·초기설정·커밋·브랜치·체리픽 실습 내용을 추가해 나갑니다.)

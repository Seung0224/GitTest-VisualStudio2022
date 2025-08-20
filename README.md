# Git 학습 Step-by-Step

---

## 1단계: Git 초기 세팅 (Visual Studio + Git Bash)

### 1-1) Git 저장소 초기화

```bash
git init
```

### 1-2) 사용자 정보 등록

```bash
git config --global user.name "YourName"
git config --global user.email "you@example.com"
```

### 1-3) 현재 설정 확인

```bash
git config --list
```

### 1-4) 원격 저장소 연결

```bash
git remote add origin https://github.com/<YOUR_ID>/<RepoName>.git
git remote -v
```

### 1-5) .gitignore 파일 생성

```bash
touch .gitignore
```

### 1-6) .gitignore 파일 내용 추가

```bash
nano .gitignore
```

### 1-7) .gitignore 파일 내용 수정 (Ctrl+O를 눌러 파일을 열고 복사후 Ctrl+S 후 종료

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

### 1-8) .gitignore 적용 확인

```bash
git check-ignore -v bin/Debug/*
```

### 1-9) 초기 커밋

```bash
git add .
git commit -m "chore: initial commit (WinForms .NET Framework 4.8.1 - GitTest)"
```

### 1-10) 원격 저장소로 푸시

```bash
git push -u origin main
```

---

## 2단계: Commit & Checkout 실습 (버튼 추가 예제)

### Step 1: 버튼1 추가 → 커밋

```bash
git add .
git commit -m "feat: Add button1"
```

### Step 2: 버튼2 추가 → 커밋

```bash
git add .
git commit -m "feat: Add button2"
```

### Step 3: 버튼3 추가 → 커밋

```bash
git add .
git commit -m "feat: Add button3"
```

### Step 4: 로그 확인

```bash
git log --oneline --decorate --graph
```

예시 출력:

```
acf51d5 (HEAD -> main) feat: Add button3
f243c69 feat: Add button2
ab42df9 feat: Add button1
e7089a6 (origin/main) chore: initial commit
```

### Step 5: Checkout으로 시간여행

```bash
git checkout ab42df9   # 버튼1 시점으로 이동
```

다시 최신으로 돌아오기:

```bash
git switch main
```

---

## 3단계: 특정 커밋만 선택해서 반영하기 (Cherry-pick / Revert)

### ▶️ Revert 방식으로 버튼2만 제외하기

```bash
# 1) 모든 버튼이 들어있는 브랜치(예: main)에서 파생
git switch -c no-button2

# 2) 버튼2 커밋만 되돌리기
git revert f243c69     # "feat: Add button2"

# (디자이너 충돌 나면 한 번만 해결 → 저장 →)
git add GitTest/Form1.Designer.cs
git commit   # (revert 커밋 완료)

# → 이제 no-button2 브랜치는 1·3·4만 포함

# 3) 나중에 다시 버튼2도 포함(1~4 전체)로 복귀할 때
git switch no-button2
git log --oneline     # 여기서 방금 만든 "revert B2" 커밋 해시를 찾는다: R_B2
git revert <R_B2>     # 되돌린 것을 되돌리기 = 버튼2를 되살림
```

---

## 4단계: GitHub에 올리기 (Push & 동기화)

### 4-1) 원격 저장소 확인

```bash
git remote -v
```

없으면 추가:

```bash
git remote add origin https://github.com/Seung0224/GitTest-VisualStudio2022.git
```

### 4-2) 브랜치별로 올리기

```bash
git push -u origin main
```

```bash
git push -u origin no-button2
```

### 4-3) 한꺼번에 모든 브랜치 올리기

```bash
git push --all origin
```

### 4-4) 원격과 충돌 시 해결 (rebase)

원격에 커밋이 있어 push가 거절될 때:

```bash
git pull --rebase origin main
# 충돌 해결 후
git add <파일>
git rebase --continue
```

그 후 다시 push:

```bash
git push -u origin main
```

---

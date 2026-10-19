# ai4_lecture
# 로컬 작업 폴더 설정부터 Git 원격 저장소 푸시까지

로컬 PC에 작업 폴더를 만들고, VS Code에서 코드를 작성한 뒤 Git 원격 저장소에 업로드하는 과정입니다.

> 준비 사항: Git과 VS Code를 설치하고, GitHub 등 사용할 Git 호스팅 서비스에 로그인합니다. 아래 명령어의 이름, 이메일, 폴더 경로, 저장소 URL은 본인 환경에 맞게 바꿔 입력합니다.

## 9. 로컬 PC의 작업 폴더 설정

프로젝트를 저장할 폴더를 만들고 해당 폴더로 이동합니다.

```bash
mkdir my-project
cd my-project
```

이미 작업 폴더가 있다면 새로 만들지 않고 해당 폴더를 사용합니다.

## 10. Git 원격 Repository 생성

GitHub 등 Git 호스팅 서비스에서 새 원격 저장소를 생성합니다.

1. **New repository**를 선택합니다.
2. 저장소 이름과 공개 범위(Public / Private)를 설정합니다.
3. **Create repository**를 선택합니다.
4. 생성된 저장소의 HTTPS 또는 SSH URL을 복사합니다.

> 이 문서처럼 로컬에서 첫 커밋을 만든 뒤 푸시할 경우, 원격 저장소는 README, `.gitignore`, 라이선스 파일 없이 빈 상태로 생성하면 진행이 간단합니다.

## 11. VS Code에서 작업 폴더 열기

VS Code에서 **파일 → 폴더 열기**를 선택하고 9번에서 준비한 폴더를 엽니다.

터미널에서 아래 명령어로 열 수도 있습니다.

```bash
code .
```

`code` 명령어가 인식되지 않으면 VS Code의 메뉴를 이용합니다. 이후 명령어는 VS Code의 **터미널 → 새 터미널**에서 실행합니다. 터미널의 현재 위치가 프로젝트 폴더인지 확인합니다.

## 12. Git 사용자 이름 및 이메일 설정

커밋 작성자 정보로 사용할 이름과 이메일을 설정합니다. 사용자 이름 설정 키는 `user.name`입니다.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

설정값을 확인합니다.

```bash
git config --global user.name
git config --global user.email
```

> `--global` 설정은 현재 PC 사용자 계정의 모든 Git 저장소에 기본으로 적용됩니다. 특정 프로젝트에만 다른 정보를 적용하려면 13번의 초기화 이후, 해당 폴더에서 `--global`을 빼고 설정합니다. 이 정보는 커밋 작성자 정보이며 원격 저장소 로그인 정보와는 별개입니다.

## 13. Git 저장소 초기화

프로젝트 폴더에서 Git 저장소를 초기화합니다.

```bash
git init
```

`.git` 폴더가 생성되며 Git이 해당 프로젝트의 변경 이력을 관리할 수 있게 됩니다.

## 14. 기본 브랜치 이름을 main으로 변경

현재 브랜치 이름을 `main`으로 설정합니다.

```bash
git branch -M main
```

## 15. 원격 Repository 연결

10번에서 복사한 원격 저장소 URL을 `origin`이라는 이름으로 등록합니다.

```bash
git remote add origin https://github.com/your-account/my-project.git
```

연결된 원격 저장소를 확인합니다.

```bash
git remote -v
```

> `origin`이 이미 등록되어 있어 URL을 변경해야 한다면 `git remote set-url origin <저장소-URL>`을 사용합니다.

## 16. 코드 커밋

프로젝트 파일을 작성하고 저장합니다. 커밋 전에 `.gitignore`에 제외할 항목을 지정합니다. 비밀번호, API 키, `.env` 등 민감한 정보와 불필요한 생성 파일이 포함되지 않도록 확인합니다.

먼저 변경 사항을 확인합니다.

```bash
git status
```

커밋할 파일을 스테이징하고 내용을 확인한 뒤 첫 커밋을 생성합니다.

```bash
git add .
git diff --cached
git commit -m "Initial commit"
```

- `git add .`: 현재 폴더와 하위 폴더의 변경 사항을 스테이징합니다. `.gitignore`에 지정된 미추적 파일은 제외됩니다.
- `git diff --cached`: 스테이징된 변경 내용을 확인합니다.
- `git commit`: 스테이징된 변경 사항을 로컬 저장소의 이력으로 기록합니다.

> 커밋할 파일이 없으면 첫 커밋을 만들 수 없습니다. README나 프로젝트 코드 등 파일을 하나 이상 작성하고 저장합니다.

## 17. 원격 저장소에 푸시

로컬 `main` 브랜치의 커밋을 원격 저장소로 업로드합니다.

```bash
git push -u origin main
```

첫 푸시 과정에서 인증이 필요할 수 있습니다. HTTPS는 호스팅 서비스가 지원하는 로그인 또는 토큰 인증을, SSH는 등록된 SSH 키를 사용합니다.

`-u`는 로컬 `main` 브랜치가 추적할 원격 브랜치를 설정합니다. 이후 같은 브랜치에서는 아래 명령어로 푸시할 수 있습니다.

```bash
git push
```

푸시 완료 후 원격 저장소 페이지에서 파일과 커밋이 업로드되었는지 확인합니다.

> 원격 저장소에 이미 커밋이 있으면 푸시가 거절될 수 있습니다. 이 경우 원격 변경 이력을 확인하고 로컬 이력과 통합한 뒤 다시 푸시합니다.

## 이후 작업 시 반복할 순서

코드를 수정하고 저장한 뒤 다음 순서로 변경 사항을 기록하고 업로드합니다.

```bash
git status
git add .
git diff --cached
git commit -m "변경 내용을 설명하는 메시지"
git push
```

---
type: system
status: active
created: 2026-07-16
updated: 2026-07-16
tags:
  - setup
---

# 초기 연결 안내

이 설정은 처음 한 번만 수행합니다. 평소에는 두 커스텀 GPT와 대화하고 Obsidian을 열어 두면 됩니다.

## 전체 흐름

```text
ChatGPT 커스텀 GPT
  ↕ GitHub Action으로 직접 읽기·쓰기
GitHub 비공개 저장소
  ↕ Obsidian Git이 자동 pull·commit·push
Obsidian Vault: neuro tranning
```

GPT는 Git 명령으로 push하지 않습니다. GPT가 GitHub API로 노트를 작성하면 GitHub에 즉시 커밋됩니다. Obsidian Git이 그 커밋을 자동 pull합니다. Obsidian에서 바꾼 노트는 Obsidian Git이 자동 commit·push합니다.

## 준비물

- ChatGPT Plus 계정
- GitHub 무료 계정
- macOS용 Obsidian 데스크톱
- 이 `neuro tranning` 폴더

비밀번호와 GitHub token은 이 Vault, ChatGPT 대화, 메모 앱에 저장하지 않습니다.

## 1단계: Vault 열기

1. Obsidian을 실행합니다.
2. `Open folder as vault` 또는 `폴더를 Vault로 열기`를 선택합니다.
3. 이 `neuro tranning` 폴더를 선택합니다.
4. 왼쪽 파일 목록에서 `README.md`와 `99 System`이 보이는지 확인합니다.

## 2단계: GitHub 비공개 저장소 만들기

1. [GitHub 새 저장소](https://github.com/new)를 엽니다.
2. Repository name을 `neuro-tranning`으로 입력합니다.
3. Visibility를 `Private`로 선택합니다.
4. README, `.gitignore`, License 자동 생성을 선택하지 않고 빈 저장소로 만듭니다.
5. 저장소 주소 `https://github.com/2rd6mws7zw-a11y/neuro-tranning.git`을 확인합니다.

저장소를 만들었다고 해서 로컬 Vault가 자동 연결되는 것은 아닙니다. 아래 Obsidian Git 초기 연결까지 완료해야 합니다.

## 3단계: GitHub 전용 token 만들기

1. GitHub에서 `Settings → Developer settings → Personal access tokens → Fine-grained tokens`로 이동합니다.
2. `Generate new token`을 선택합니다.
3. 이름을 `ChatGPT Obsidian Vault`로 입력합니다.
4. 만료 기간을 선택합니다. 만료되면 새 token으로 ChatGPT Action 인증을 갱신해야 합니다.
5. Repository access에서 `Only select repositories`를 선택합니다.
6. `neuro-tranning` 하나만 선택합니다.
7. Repository permissions에서 `Contents`를 `Read and write`로 설정합니다.
8. 나머지 권한은 추가하지 않습니다.
9. token을 생성하고 안전한 암호 관리 도구에 보관합니다.

token은 이 문서나 ChatGPT 대화에 붙여넣지 않습니다. 두 GPT의 Action 인증 입력란에만 직접 입력합니다.

## 4단계: 뉴로트레이닝 스터디 GPT 연결

이 작업은 ChatGPT 웹에서 수행합니다.

1. ChatGPT의 `뉴로트레이닝 스터디 GPT`를 엽니다.
2. GPT 이름 옆 메뉴에서 `Edit GPT` 또는 `GPT 편집`을 선택합니다.
3. Configure의 Instructions를 열고 다음 파일의 본문을 붙여넣습니다.
   - `99 System/GPT Setup/neurotraining-study-gpt-instructions.md`
4. `GITHUB_OWNER` 값이 `2rd6mws7zw-a11y`로 되어 있는지 확인합니다.
5. Actions에서 `Create new action` 또는 `새 Action`을 선택합니다.
6. 다음 파일의 JSON 전체를 Schema에 붙여넣습니다.
   - `99 System/GPT Setup/github-action-openapi.json`
7. Authentication을 `API Key`로 선택합니다.
8. Auth type 또는 전송 방식은 `Bearer`를 선택합니다.
9. 앞에서 만든 GitHub token을 인증 입력란에 직접 붙여넣습니다.
10. `searchVault`, `readVaultFile`, `writeVaultFile` 세 작업이 표시되는지 확인합니다.
11. GPT를 Private 상태로 저장합니다.

### Preview 테스트

다음 문장을 입력합니다.

```text
GitHub Vault의 README.md를 읽고 제목만 알려줘. 아직 어떤 파일도 수정하지 마.
```

읽기 Action의 승인을 요구하면 대상이 `api.github.com`인지 확인한 뒤 승인합니다. README의 제목 `neuro tranning`을 답하면 읽기 연결이 정상입니다.

## 5단계: 독학골프가이드 GPT 연결

1. `독학골프가이드 GPT`의 편집 화면을 엽니다.
2. 다음 파일의 본문을 Instructions에 붙여넣습니다.
   - `99 System/GPT Setup/self-golf-guide-gpt-instructions.md`
3. `GITHUB_OWNER` 값이 `2rd6mws7zw-a11y`로 되어 있는지 확인합니다.
4. 뉴로트레이닝 GPT와 동일한 OpenAPI JSON을 Actions Schema에 붙여넣습니다.
5. Authentication을 `API Key / Bearer`로 설정합니다.
6. 동일한 GitHub token을 인증 입력란에 직접 붙여넣습니다.
7. 세 작업이 표시되는지 확인하고 GPT를 Private 상태로 저장합니다.
8. 위와 동일하게 README 읽기를 시험합니다.

ChatGPT가 쓰기 전에 확인을 요청할 수 있습니다. 계정에 `Always allow`가 표시되더라도 대상 도메인과 쓰는 경로를 확인한 뒤 선택합니다.

## 6단계: Obsidian Git 설치

1. Obsidian에서 `Settings → Community plugins`를 엽니다.
2. Restricted mode를 해제하고 커뮤니티 플러그인을 허용합니다.
3. Browse에서 `Obsidian Git`을 검색합니다.
4. 설치 후 Enable을 선택합니다.
5. Command palette를 열고 `Obsidian Git: Initialize a new repo`를 실행합니다.
6. `Obsidian Git: Edit remotes`를 실행합니다.
7. remote 이름은 `origin`, 주소는 `https://github.com/2rd6mws7zw-a11y/neuro-tranning.git`로 입력합니다.
8. 기본 브랜치가 `main`인지 확인합니다.
9. `Obsidian Git: Commit-and-sync`를 실행하여 초기 파일을 GitHub에 올립니다.

GitHub 로그인을 요구하면 브라우저 또는 macOS 자격 증명 창에서 본인이 직접 승인합니다. 인증 정보를 Vault 파일에 쓰지 않습니다.

### 권장 자동화 설정

Obsidian Git 설정에서 다음 값을 사용합니다. 플러그인 버전에 따라 메뉴 문구가 조금 다를 수 있습니다.

```text
Pull updates on startup: 켜기
Auto pull interval: 2분
Auto commit-and-sync interval: 5분
Commit message: vault backup {{date}}
Push on backup: 켜기
Pull before push: 켜기
Conflict 또는 force overwrite: 자동 덮어쓰기 끄기
```

자동 동기화는 Obsidian 데스크톱이 실행 중이고 인터넷 연결과 GitHub 인증이 정상일 때 작동합니다.

## 7단계: 평소 사용

### 새 대화 시작

```text
이어서 시작
```

GPT가 최근 대화 요약과 관련 지식을 검색한 뒤 현재 상태를 설명합니다.

### 평범한 질문

별도 형식 없이 평소처럼 질문합니다. 다음 사용자 메시지를 보내면 GPT가 직전 질문과 답변을 구조화 요약으로 저장하도록 지시되어 있습니다.

### 대화 종료

```text
정리하고 저장
```

마지막 질문과 답변까지 저장하고 Vault 경로를 알려주는지 확인합니다.

## 문제 해결

### GPT가 401 오류를 표시함

GitHub token이 잘못되었거나 만료되었습니다. GPT 편집기의 Action Authentication에서 새 token으로 교체합니다.

### GPT가 403 오류를 표시함

token이 `neuro-tranning` 저장소를 선택했는지, Contents가 Read and write인지 확인합니다.

### GPT가 404 오류를 표시함

Instructions의 GitHub 사용자명, 저장소명 `neuro-tranning`, 기본 브랜치 `main`, 파일 경로를 확인합니다.

### GPT가 409 오류를 표시함

다른 곳에서 파일이 변경된 충돌입니다. 기존 파일을 덮어쓰지 말고 타임스탬프가 붙은 `-draft.md` 파일로 저장하게 합니다.

### GitHub에는 있는데 Obsidian에 안 보임

Obsidian이 열려 있는지 확인하고 Command palette에서 `Obsidian Git: Pull`을 한 번 실행합니다. 성공하면 자동 pull 간격 설정을 확인합니다.

### Obsidian 변경이 GPT에 안 보임

Obsidian Git 상태를 확인하고 `Commit-and-sync`를 한 번 실행합니다. GitHub 웹에서 파일이 올라왔는지 확인한 후 GPT에 다시 검색시킵니다. GitHub 검색 색인에는 짧은 지연이 있을 수 있습니다.

### Action이 실행되지 않음

다음처럼 명시적으로 요청합니다.

```text
Vault를 검색해서 답하고, 이번 대화를 구조화 요약으로 저장해줘.
```

모든 저장을 모델이 무조건 호출한다고 보장할 수 없으므로 대화 종료 시 `정리하고 저장`을 사용합니다.

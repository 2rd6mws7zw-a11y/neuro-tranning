---
type: system
status: active
created: 2026-07-16
updated: 2026-07-16
tags:
  - verification
---

# 양방향 연결 검증 체크리스트

모든 테스트는 개인 정보가 없는 임시 내용으로 실행합니다.

## 1. Obsidian에서 GitHub로 자동 push

준비:

- `00 Inbox/connection-test.md`를 만들고 `Obsidian to GitHub test`라고 입력합니다.

실행:

- 저장 후 최대 5분 기다립니다.
- GitHub 웹의 `neuro-tranning` 저장소를 새로고침합니다.

합격:

- 같은 경로와 내용의 파일이 GitHub에 보입니다.

실패 시:

- Obsidian Git 상태, remote `origin`, commit-and-sync 간격, GitHub 인증을 확인합니다.

## 2. 뉴로트레이닝 GPT가 Obsidian 노트 읽기

실행:

```text
Vault에서 connection-test.md를 찾아 내용을 그대로 말해줘. 수정하지 마.
```

합격:

- GPT가 `Obsidian to GitHub test`를 읽고 Vault 경로를 표시합니다.

실패 시:

- Action 인증, GitHub 사용자명, 저장소명, searchVault 결과를 확인합니다.

## 3. 뉴로트레이닝 GPT가 학습 노트 쓰기

실행:

```text
연결 테스트용 학습 노트를 20 Study/Study Notes/2026-07-16-gpt-write-test.md에 만들어줘. 내용은 GPT to Obsidian study test로 하고 저장 경로를 알려줘.
```

합격:

- GitHub에 새 파일이 생기고 최대 2분 뒤 Obsidian에 나타납니다.

실패 시:

- writeVaultFile 승인, token의 Contents read/write 권한, Obsidian 자동 pull을 확인합니다.

## 4. 스터디 지식을 유튜브 GPT가 읽기

준비:

- 앞 테스트 노트가 GitHub에 존재하는지 확인합니다.

실행:

```text
20 Study에서 gpt-write-test 노트를 찾아 읽고, 이 자료를 활용한 3단계 골프 영상 구성안을 채팅에만 보여줘. 아직 저장하지 마.
```

합격:

- 독학골프가이드 GPT가 정확한 스터디 노트 경로를 표시하고 3단계 구성안을 답합니다.

실패 시:

- 골프 GPT의 Instructions와 읽기 Action 연결을 확인합니다.

## 5. 유튜브 구성안을 Obsidian으로 저장

실행:

```text
방금 구성안을 30 YouTube/Outlines/2026-07-16-connection-test-outline.md에 저장하고 사용한 스터디 노트 경로를 포함해줘.
```

합격:

- GitHub와 Obsidian의 해당 경로에 파일이 나타나며 원본 스터디 노트 경로가 기록됩니다.

실패 시:

- 쓰기 승인, token 권한, 자동 pull을 확인합니다.

## 6. 두 GPT 대화 기억 분리

실행:

- 뉴로트레이닝 GPT와 골프 GPT에서 각각 한 번씩 `정리하고 저장`을 입력합니다.

합격:

- 뉴로트레이닝 대화는 `40 Conversations/Neurotraining Study GPT/`에만 저장됩니다.
- 골프 대화는 `40 Conversations/Self Golf Guide GPT/`에만 저장됩니다.

실패 시:

- 두 GPT에 서로 다른 Instructions가 입력되었는지 확인합니다.

## 7. 새 대화에서 기억 이어받기

실행:

- 각 GPT에서 새 대화를 시작합니다.
- `이어서 시작`이라고 입력합니다.

합격:

- GPT가 최근 대화의 목표, 결정, 다음 작업을 불러와 요약합니다.

실패 시:

- 최근 대화 파일이 GitHub에 존재하는지, searchVault가 해당 폴더를 검색했는지 확인합니다.

## 8. 충돌 시 덮어쓰기 방지

준비:

- GitHub 웹에서 테스트 노트를 수정하되 Obsidian에서는 아직 pull하지 않습니다.

실행:

- GPT에 같은 테스트 노트를 수정하도록 요청합니다.

합격:

- SHA 충돌이 나면 GPT가 기존 파일을 강제로 덮어쓰지 않습니다.
- 타임스탬프가 붙은 `-draft.md` 새 파일을 만들거나 충돌 사실을 보고합니다.

실패 시:

- GPT Instructions의 최신 SHA 확인 및 충돌 규칙을 확인합니다.

## 완료 기준

- [ ] Obsidian → GitHub 자동 push 성공
- [ ] GitHub → Obsidian 자동 pull 성공
- [ ] 스터디 GPT 읽기 성공
- [ ] 스터디 GPT 쓰기 성공
- [ ] 골프 GPT가 스터디 자료 재사용
- [ ] 유튜브 결과물 저장 성공
- [ ] GPT별 대화 요약 분리 성공
- [ ] 새 대화에서 기억 불러오기 성공
- [ ] 충돌 시 기존 파일 보호

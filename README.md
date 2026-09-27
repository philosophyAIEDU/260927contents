# 콘텐츠 스튜디오 스타터

내 콘텐츠를 모으고, 다음 콘텐츠 아이디어를 받고, 초고까지 만들어 주는 **Claude Code 작업 폴더**입니다. 유튜브 대본, 뉴스레터, 스레드를 만드는 크리에이터를 위해 만들었습니다.

```
① 모으기 (Input)      내 대본·뉴스레터·스레드를 정리해 Firebase에 올린다     /ingest
② 분석                내 말투와 잘 된 콘텐츠의 패턴을 찾는다                /analyze-style
③ 아이디어            모아 둔 콘텐츠를 근거로 다음 주제 5개를 제안한다       /topic-ideas
④ 초고 (Output)       주제 한 줄로 초고를 쓰고, 검수한 뒤 자동으로 보관한다  /thread-draft ...
⑤ 확인                웹 관리자 페이지에서 Input과 Output을 본다            admin/index.html
```

초고는 완성본이 아니라 **"20% 고칠 게 남은 초고"** 입니다. 마지막 손질과 발행은 언제나 내가 합니다.

## 이런 점이 다릅니다
- **내 말투로 씁니다.** `voice.md`(말투)와 `structure.md`(잘 된 패턴)를 내 콘텐츠에서 뽑아서 초고의 기준으로 씁니다.
- **지어내지 않습니다.** 수치는 내가 올린 자료에 있는 것만 쓰고, 없으면 "확인 필요"로 표시합니다.
- **자동으로 검수합니다.** 초고를 쓰면 말투 검수(`voice-checker`)와 과장·개인 노출 검수(`risk-checker`)가 따로 돕니다.
- **안전 장치가 있습니다.** 업로드 전에 필수 태그, 중복, 개인정보를 검사하고, 기본은 미리보기(dry-run)입니다. 댓글은 작성자 정보 없이 저장합니다.

## 시작하기

**[TUTORIAL.md](TUTORIAL.md)를 위에서부터 순서대로 따라 하세요.** 처음이라면 약 40분 걸립니다. 준비물은 아래와 같습니다.

- [Claude Code](https://claude.com/claude-code) 사용 가능한 계정
- [Node.js](https://nodejs.org) 20.6 이상 (LTS 권장)
- 구글 계정 (Firebase 무료 플랜으로 충분합니다)

## 폴더 안내

| 폴더·파일 | 역할 |
|---|---|
| `raw/` | 내 원본 파일을 넣는 곳 (수정하지 않고, git에 올라가지 않음) |
| `processed/` | 정리·태깅된 콘텐츠 (Input에 올라가는 JSON) |
| `drafts/` | 초고 (`thread/`, `newsletter/`, `script/`) |
| `reports/` | 작업 기록 |
| `voice.md`, `structure.md` | 내 말투, 잘 된 패턴 (`/analyze-style`이 채움) |
| `scripts/` | 업로드·검수 스크립트 (Claude가 알아서 실행) |
| `admin/index.html` | Input·Output을 보는 관리자 웹 페이지 |
| `firestore.rules` | Firebase 보안 규칙 (나만 읽고 쓰게) |
| `.claude/` | Claude Code용 명령어(스킬)와 검수 에이전트 |
| `CLAUDE.md` | Claude가 매번 읽는 규칙 |
| `GUIDE_FOR_CLAUDE.md` | Claude가 사용자를 안내하는 방법 (진행 상황 파악, 브랜드 맞춤 질문, 안전 원칙) |
| `examples/` | 연습용 예시 대본 |

`/menu`를 입력하면 전체 명령어를 볼 수 있습니다.

## 꼭 지켜 주세요
- **서비스 계정 키(`keys/`)와 `.env`는 절대 GitHub에 올리지 마세요.** `.gitignore`가 막아 주지만, 그 설정을 지우지 마세요.
- 이 저장소를 내려받아 **내 콘텐츠를 넣은 뒤에는 내 저장소를 private으로** 두세요. 내 말투 파일(`voice.md`)에는 내 문장이 들어갑니다.
- 내가 직접 만든 콘텐츠만 넣으세요. 타인의 글이나 유료 콘텐츠는 넣지 않습니다.

## 라이선스
MIT License. 자유롭게 쓰고 고쳐도 됩니다.

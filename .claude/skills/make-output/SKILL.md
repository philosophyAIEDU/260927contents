---
name: make-output
description: 올라간 콘텐츠(Contents Input)를 참고해서 새 결과물(대본 초안, 스레드, 뉴스레터, 요약 등)을 만들고 관리자 전용 Contents Output에 저장할 때 쓴다. "이 대본으로 스레드 만들어줘", "뉴스레터 초안 써줘", "Output에 저장해줘"라고 하면 실행한다. drafts/에 있는 초고 파일을 Output에 올릴 때도 쓴다. 새 초고를 쓰는 일은 /thread-draft, /newsletter-draft, /script-draft, /repurpose를, 원본 콘텐츠를 정제해서 올리는 일은 /ingest를 쓴다.
---

# /make-output — 결과물 작성과 Contents Output 저장

작업 폴더: 이 프로젝트 폴더(저장소를 내려받은 폴더). Contents Output은 관리자 전용 Firestore 컬렉션 `contents_output`이며 관리자 페이지(`admin/index.html`)의 Contents Output 탭에서 보인다.

## 절차
1. **요청 파악**: 어떤 결과물인지(종류: 스레드/뉴스레터/대본 초안/요약 등), 참고할 Input 문서(id), 분량과 어조를 확인한다. 참고 문서가 없으면 `processed/`에서 관련 후보를 제안하고 고르게 한다.
2. **참고 자료 읽기**: `processed/<id>.json`의 `body`와 태그를 읽는다. 결과물은 사용자의 콘텐츠에서만 근거를 가져온다. 외부 자료를 섞으면 어느 부분인지 밝히고 확인받는다 (규칙 3: 타인의 글·유료 콘텐츠는 넣지 않는다).
3. **초안 작성**: 참고 문서의 내용과 핵심 메시지에 맞춰 쓴다. 성과가 좋은 콘텐츠(`performance_grade: 상`)의 주제·구성을 참고하되 문장을 그대로 복사하지 않는다. 사실이 아닌 수치나 인용을 지어내지 않는다.
4. **보여주고 확인받기**: 초안을 사용자에게 보여주고 수정 요청을 반영한다. 확정 전에는 저장하지 않는다.
5. **로컬 저장**: 확정본을 `processed/_outputs/<슬러그>.json`으로 저장한다.
   `{"title": "...", "type": "스레드", "sourceIds": ["script-01"], "body": "..."}`
6. **업로드**: `node scripts/save-output.mjs --file processed/_outputs/<슬러그>.json`(dry-run, `sourceIds`가 `processed/`에 실제 있는지 검증) → 확인받은 뒤 `node --env-file=.env scripts/save-output.mjs --file <경로> --commit`. 키 파일(`keys/`)의 내용은 읽지 않는다. 경로는 `.env`에 있다.
7. **기록**: `reports/ingest-log.md`에 날짜, 결과물 제목·종류, 참고 id, 저장 결과를 추가한다.

## `drafts/`의 초고 파일을 올릴 때
- 인자가 `drafts/...md` 경로이면 새로 쓰지 않고 그 파일을 올린다 (1~3단계 생략).
- `body`에는 `## 초고` 아래 본문만 넣는다. `## 적용한 규칙`, `## 검수 메모`는 넣지 않는다 (필요하면 `meta.review`에 판정 두 줄만).
- `title`은 초고 파일의 첫 줄 제목, `type`은 채널(스레드/뉴스레터/유튜브 대본)로 한다. `sourceIds`는 파일 메타의 "근거 자료" id를 쓴다.
- 검수 메모에 **미해결 항목이 있으면** 올리기 전에 알리고 확인받는다.

## 금지
- 댓글 작성자 정보를 결과물에 인용하지 않는다 (규칙 2). 댓글을 인용할 때는 내용만 쓴다.
- 사용자 확인 없이 `--commit` 하지 않는다.

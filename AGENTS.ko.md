# OpenCode 기여자를 위한 가이드

이 문서는 OpenCode 코드베이스에서 작업할 때 따라야 할 스타일 가이드와 규칙을 설명합니다.

## 브랜치 이름

최대 3 단어로 구성된 짧은 브랜치 이름을 사용하며, 하이픈으로 구분합니다. 슬래시나 `feat/`, `fix/` 와 같은 타입 접두사를 사용하지 않습니다.

예시: `session-recovery`, `fix-scroll-state`, `regenerate-sdk`

## 커밋 및 PR 제목

conventional commit 스타일의 메시지 사용: `type(scope): summary`

유효한 타입: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`  
스코프는 선택 사항. 영향받은 패키지나 영역을 명시 (예: `core`, `opencode`, `tui`, `app`, `desktop`, `sdk`, `plugin`)

예시:
- `fix(tui): simplify thinking toggle styling`
- `docs: update contributing guide`
- `chore(sdk): regenerate types`

사용자 대상 `feat`, `fix`, `perf` PR 의 경우, PR 본문에 `### Visual` 섹션 아래 작은 루핑 애니메이션 SVG 추가 (240×72 크기). `currentColor` 와 opacity 로 라이트/다크 모드 모두 작동하게 작성.

## 스타일 가이드

### 일반 원칙

- 하나의 함수에 담을 수 있으면 분리하지 않기
- 경계에서 한 번만 유효성 검사하기
- 한 번만 사용하는 값은 변수로 추출하지 않기
- `try`/`catch` 는 가능한 한 피하기
- `any` 타입 사용 피하기
- 가능한 한 Bun API 사용 (예: `Bun.file()`)
- 타입 추론에 의존하기
- `for` 루프보다 함수형 배열 메서드 (`flatMap`, `filter`, `map`) 선호

```ts
// 좋음
const journal = await Bun.file(path.join(dir, "journal.json")).json()

// 나쁨
const journalPath = path.join(dir, "journal.json")
const journal = await Bun.file(journalPath).json()
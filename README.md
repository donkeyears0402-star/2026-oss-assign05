# 2026 OSS Assignment 05

21901037 이준형

## Deployment

- Vercel URL: https://2026-oss-assign05-pied.vercel.app

## Key Learning

1. `getElementById`, `createElement`, `appendChild`, `remove`로 JavaScript에서 화면 요소를 직접 만들고 지울 수 있다.
2. `addEventListener`로 버튼 클릭, 폼 제출, 키 입력 이벤트를 처리하고, `preventDefault()`로 폼 제출 시 새로고침을 막을 수 있다.
3. 데이터는 배열에 저장하고, 추가/수정/삭제 후 `render()`로 화면을 다시 그리면 데이터와 화면이 항상 같게 유지된다.

## CRUD Service

- **주제**: 영화 감상 기록
- **입력 필드**: 제목, 감독, 장르(select), 개봉연도, 평점(1~5)
- **Create**: [저장] 버튼을 누르면 유효성 검사 후 `push()`로 배열에 추가하고 `render()`, 폼 초기화
- **Read**: 페이지 로드 시와 추가/수정/삭제 후 `render()`에서 `forEach()`로 배열을 테이블에 출력
- **Update**: [수정] 버튼을 누르면 `find()`로 영화를 찾아 폼에 값을 채우고, [수정 완료]를 누르면 유효성 검사 후 배열 값을 바꾸고 `render()`
- **Delete**: [삭제] 버튼을 누르면 `confirm("삭제하시겠습니까?")`로 확인 후 `findIndex()`, `splice()`로 배열에서 삭제하고 `render()`
- **유효성 검사 (추가, 수정 공통)**
  - 제목, 감독 필수 입력
  - 제목 30자 이내
  - 장르 선택 여부
  - 개봉연도 1900~2026, 평점 1~5 범위
  - 같은 제목 중복 확인 (`filter()`)

## JavaScript

- **js_dynamic.html**: 입력한 값을 `<li>`로 만들어 목록에 추가하고, 각 항목의 [삭제] 버튼으로 삭제. 추가 후 입력칸 비우기, Enter 키로도 추가 가능
- **crud.html**
  - 배열 메서드: `push`, `forEach`, `find`, `findIndex`, `filter`, `splice`
  - `editId` 변수로 추가 모드와 수정 모드를 구분
  - `validate()` 함수 하나를 추가와 수정에서 같이 사용
- **style.css**: 레이아웃, 폼, 입력창, 버튼, 테이블, 수정/삭제 버튼 색상, hover 효과

## AI / Search Usage

| Tool | Purpose | Used | What I Learned |
| --- | --- | --- | --- |
| GPT (OpenAI) | 코드 작성 도움, 단계별 설명 | CRUD 함수 구조, 유효성 검사, 오류 원인 확인 | 배열을 바꾸고 `render()`를 다시 호출하는 구조가 관리하기 쉽다 |
| MDN 검색 | 메서드 사용법 확인 | `find`, `findIndex`, `splice`, `isComposing` | `find`는 요소를, `findIndex`는 위치를 반환한다 |

## Problem & Solution

1. **공백만 입력해도 목록에 추가됨**: `trim()`으로 앞뒤 공백을 지운 뒤 빈 값인지 검사했다.
2. **한글 입력 후 Enter를 누르면 두 번 추가됨**: 한글 조합 중에도 keydown이 발생해서 `event.isComposing`이 true일 때는 추가하지 않도록 했다.
3. **수정 중인 영화를 삭제하면 [수정 완료] 시 오류 발생**: 삭제할 때 그 영화가 수정 중이면 `editId`를 `null`로 바꾸고 폼을 초기화했다.

## Reflection

지난 과제에서는 폼 화면만 만들었는데, 이번에는 입력한 값이 실제로 추가되고 수정, 삭제까지 되어서 간단한 웹 서비스를 만든 느낌이었다. 처음에는 수정할 때 테이블 글자를 직접 바꿔야 하나 고민했는데, 배열 값만 바꾸고 `render()`를 다시 부르면 된다는 것을 알게 되었다. 기능을 하나씩 만들고 커밋하면서 어떤 단계에서 무엇을 바꿨는지 확인하기 쉬웠다. 지금은 새로고침하면 데이터가 처음으로 돌아가는데, 다음에는 localStorage를 사용해서 데이터를 저장해 보고 싶다.

# EPUB Studio Mobile v7.9.19 — Full Code Audit

이번 버전은 기능 추가판이 아니라 전체 코드 감사 및 런타임 오류 수정판입니다.

## 실제로 발견한 치명적 오류
1. `isVolumeHeadingLine()` 미정의 — v7.9.18에서 수정.
2. `isPartHeadingLine()` 미정의 — v7.9.18에서 수정.
3. `serializeXML()` 미정의 — v7.9.19에서 추가 수정.

`mergeEmptyChapterPartPages()`가 XML DOM을 수정한 뒤 `serializeXML()`을 호출했지만 함수가 존재하지 않아, 앞의 ReferenceError를 고친 뒤 다음 단계에서 또 중단될 수 있었습니다.

## 이번 검사 방식
- `node --check`: 전체 script 3개 문법 검사
- TypeScript `--allowJs --checkJs`: 전체 애플리케이션 스크립트의 미정의 이름 검사
- 외부 번들 `JSZip`을 제외한 애플리케이션 미정의 이름 0개
- 실제 DOM id 중복 검사
- `$()` / `getElementById()` 참조 대상 검사
- `data-target` / `data-next` 이동 대상 검사
- id가 있는 버튼 34개 이벤트 연결 검사
- 함수 중복 선언 검사
- Node VM에서 top-level 및 DOMContentLoaded 초기화 코드 실행 검사

## 신규 런타임 자체검사
페이지 로드 시 `runtimeSelfCheck()`가 다음 필수 기능을 확인합니다.
- JSZip
- DOMParser / XMLSerializer
- serializeXML
- mergeEmptyChapterPartPages
- validateGeneratedEpubBlob
- TXT / 다권 EPUB / 단일 EPUB 생성 함수
- Volume / Part / Chapter 구조 판정 함수

필수 기능이 빠졌으면 EPUB 생성 버튼을 누른 뒤 뒤늦게 ReferenceError가 나는 대신, 로드 단계에서 명확한 오류를 냅니다.

## 유지되는 기능
- 권 전용 페이지 별도 XHTML
- 자체 본문 없는 Chapter/Part를 첫 하위 화와 결합
- Chapter/Part 반복 번호 문맥 매칭
- `_999`, `_9999` 보조 문자열 무시 매칭
- `8권 (외전2)` 권 인식
- 작품 설명/설명 이미지
- 파일 선택 즉시 바이트 캐시
- 다권 EPUB CSS basename 충돌 방지 alias
- OPF/NAV/NCX/XML/ZIP/내부 링크 검사

## 제한
이 컨테이너의 Chromium headless 프로세스가 정상 종료/렌더링되지 않아 실제 모바일 브라우저 전체 클릭 자동화는 수행하지 못했습니다. 대신 정적 검사 + TypeScript 미정의 이름 검사 + Node VM 초기화 실행 검사를 함께 수행했습니다.

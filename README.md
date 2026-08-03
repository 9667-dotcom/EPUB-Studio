# EPUB Studio Mobile v6.1.0

## 전체 생성 경로 통합 수정
- TXT, 단일 EPUB, 다권 EPUB, 혼합 ZIP에서 같은 표지/설명 CSS와 XHTML 생성 함수를 사용
- makeXhtml의 body class 미적용 오류 수정
- 작품 설명 body에 hm-desc 클래스 적용
- 표지 body에 hm-cover-page 클래스 적용
- 잘못 합쳐진 TXT CSS 선택자와 중복 CSS 제거
- 작품 소개, BL 가이드, 작품 정보 섹션 및 특수문자/줄바꿈 처리 유지
- 표지와 작품 설명이 manifest/spine에 실제 등록되었는지 생성 중 검증
- 생성된 XHTML의 body class와 설명 섹션 존재를 재검증

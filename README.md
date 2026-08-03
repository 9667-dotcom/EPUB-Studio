# EPUB Studio Mobile v0.3

## 기능 1: EPUB 만들기·합본
- EPUB, TXT, ZIP(TXT) 입력
- 대표 표지, 권별 표지 선택
- 작품 설명은 캡처 이미지를 삽입하지 않고 붙여넣은 텍스트만 사용
- 권→화 목차 배정
- NAV/NCX/OPF 생성
- 기본 XML/manifest/spine 검사
- EPUB 다운로드

## 기능 2: 좌우 정렬만 제거
- 원본 EPUB의 모든 CSS 파일명·경로·개수 유지
- CSS의 text-align: justify / text-align-last: justify 제거
- XHTML/HTML 인라인 style과 align="justify" 제거
- center/left/right 등 다른 정렬은 유지
- manifest/spine/XML/ZIP CRC 검증 후 EPUB 다운로드

## GitHub Pages
저장소 root에 index.html과 .nojekyll을 업로드한 뒤
Settings → Pages → Deploy from a branch → main → /(root)를 사용합니다.

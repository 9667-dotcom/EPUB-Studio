# EPUB Studio Mobile V5.1

브라우저에서 EPUB, TXT, ZIP 파일을 분석하고 하나의 EPUB으로 구성하는 단일 HTML 도구입니다.

## 주요 기능

- `.epub`, `.txt`, `.zip` 파일 여러 개 동시 선택
- EPUB과 TXT를 섞어 선택 가능
- ZIP 내부의 TXT와 EPUB이 함께 있는 혼합 ZIP 지원
- ZIP 내부 하위 폴더의 `.txt`, `.epub` 탐색
- 원본 EPUB의 CSS, 이미지, SVG, JavaScript, 폰트 등 리소스를 원본별 독립 경로에 복사
- 원본 NAV/NCX, 붙여넣은 목차, 파일명 정보를 이용한 권·화 구성
- EPUB3 `nav.xhtml`과 EPUB2 `toc.ncx` 생성
- 표지, 작품 설명, 권 전용 페이지 구성
- 좌우 정렬 제거와 긴 문단 가독성 개선을 선택적으로 적용
- 생성 전 manifest, spine, 목차 링크, XML 구조 검사
- 생성 후 ZIP CRC, `mimetype` 위치·압축 방식·내용 검사

## GitHub Pages 배포

저장소의 GitHub Pages 배포 위치에 다음 파일을 함께 올립니다.

```text
index.html
.nojekyll
README.md
```

### 저장소 루트에서 배포하는 경우

1. GitHub 저장소의 `Settings` → `Pages`로 이동합니다.
2. `Build and deployment`에서 `Deploy from a branch`를 선택합니다.
3. 브랜치를 `main`, 폴더를 `/(root)`로 지정합니다.
4. `index.html`, `.nojekyll`, `README.md`를 저장소 최상단에 올립니다.

### docs 폴더에서 배포하는 경우

Pages 폴더를 `/docs`로 지정했다면 세 파일을 모두 `docs` 폴더 안에 넣습니다.

```text
docs/
├── index.html
├── .nojekyll
└── README.md
```

## 사용 방법

1. 배포된 GitHub Pages 주소 또는 로컬 `index.html`을 엽니다.
2. `입력 파일`에서 EPUB, TXT, ZIP 파일을 하나 이상 선택합니다.
3. `원본 분석`을 누릅니다.
4. 필요하면 표지와 작품 설명을 입력합니다.
5. `원본 목차로 자동 구성` 또는 `목차 분석·본문 배정`을 실행합니다.
6. 감지된 화, 권 배정, 표지 연결을 확인합니다.
7. 생성 전 검사에서 오류가 없는지 확인합니다.
8. `EPUB 생성`을 눌러 결과 파일을 저장합니다.

## 지원 입력

| 입력 | 지원 여부 |
|---|---|
| EPUB 1개 | 지원 |
| TXT 1개 | 지원 |
| EPUB 여러 개 | 지원 |
| TXT 여러 개 | 지원 |
| EPUB과 TXT 동시 선택 | 지원 |
| TXT만 들어 있는 ZIP | 지원 |
| EPUB만 들어 있는 ZIP | 지원 |
| TXT와 EPUB이 함께 있는 ZIP | 지원 |
| ZIP 내부 하위 폴더 | 지원 |
| ZIP 안에 다시 ZIP이 들어 있는 중첩 ZIP | 미지원 |

## 입력 순서와 권 구성

- 원본 NAV/NCX가 있으면 해당 순서를 우선 사용합니다.
- 붙여넣은 목차가 있으면 목차 순서를 적용합니다.
- 위 정보가 없으면 ZIP 내부 경로와 파일명에서 권 번호를 추정합니다.
- 자동 결과가 정확하지 않은 경우 화면에서 새 권을 만들고 화를 직접 이동할 수 있습니다.

## 원본 보존 방식

혼합 입력을 합칠 때 각 EPUB의 내부 파일은 서로 다른 원본 폴더에 복사됩니다. 같은 이름의 CSS나 이미지가 여러 EPUB에 있어도 충돌하지 않도록 경로를 분리하며, XHTML에서 사용하는 상대경로도 함께 조정합니다.

`좌우 정렬만 제거` 또는 `긴 문단 가독성 개선`을 켜지 않으면 원본 본문과 CSS를 임의로 변경하지 않는 것을 기본 원칙으로 합니다.

## 주의사항

- DRM이 적용된 EPUB은 브라우저에서 정상적으로 읽을 수 없습니다.
- 매우 큰 EPUB 또는 파일 수가 많은 ZIP은 브라우저 메모리 제한의 영향을 받을 수 있습니다.
- 자동 화 인식은 제목 패턴과 원본 목차 품질에 영향을 받으므로 생성 전에 대응표를 확인해야 합니다.
- 혼합 ZIP 안의 또 다른 ZIP은 자동으로 풀지 않습니다.
- EPUB 생성 중 오류가 표시되면 미배정 화, 중복 배정, 잘못된 내부 링크를 먼저 확인합니다.

## 빈 화면이 나올 때

1. 파일명이 정확히 `index.html`인지 확인합니다.
2. GitHub Pages가 바라보는 폴더와 실제 파일 위치가 같은지 확인합니다.
3. `Ctrl + F5`로 캐시를 무시하고 새로고침합니다.
4. 브라우저 개발자 도구의 `Console`에서 JavaScript 오류를 확인합니다.
5. GitHub Pages 배포가 완료된 뒤 표시되는 실제 Pages 주소로 접속합니다.

## 파일 구성

- `index.html`: 프로그램 전체가 포함된 실행 파일
- `.nojekyll`: GitHub Pages의 Jekyll 처리를 비활성화하는 빈 파일
- `README.md`: 설치, 배포, 사용 안내

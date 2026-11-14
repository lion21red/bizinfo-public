# 공개 홈 (로그인 전 첫 화면)

정적 사이트입니다. DB에 직접 접근하지 않고 `data/*.js`만 읽습니다 (docs/LANDING_PAGE_PLAN.md 9절).

| 파일 | 만드는 곳 | 갱신 |
|---|---|---|
| `index.html`, `plan2026.html`, `board.html` | `scripts/make_public_site.py` (승인된 시안 `docs/mockups/`에서 생성) | 시안을 고칠 때 |
| `data/stats.js` (현황 집계), `data/news.js` (기업지원정보+운영자 조건의 최근 글 카드), `data/board.js` (공개 글 전체) | `scripts/build_public_data.py` | 매일 18:30 (`.github/workflows/public-site.yml`) |
| `support-*.html` (지원 유형별 12쪽), `method.html` (데이터·매칭 방법), `robots.txt` | `scripts/make_public_site.py` + `public_seo.py` | 시안을 고칠 때 |
| `board.html`의 미리 쓴 글, `news-*.html` (소식별 페이지), `sitemap.xml`, `llms.txt` | `scripts/build_public_data.py` (`public_seo.finish`) | 매일 18:30 (git 제외) |
| `data/examples.js` (실제 결과 예시), `data/plan2026.js` (2026 지원사업 목록) | 검토를 마친 고정 데이터 복사 | 필요할 때 |
| `pdf/` (정부 원문 PDF 5개) | 공개 저장소에 한 번 직접 올림 (git 제외) | 연 1회 |

로컬에서 보기: `python scripts/make_public_site.py` → `python scripts/build_public_data.py` → `index.html`을 브라우저로 연다.
`data/board.js`(게시판 공개 글)도 `build_public_data.py`가 만들며, 앱에서 글의 공개 상태가 바뀌면 워크플로를 바로 실행해 갱신한다 (`GITHUB_DISPATCH_TOKEN`이 있을 때).
`stats.js`·`news.js`·`board.js`는 만들어 쓰는 파일이라 이 저장소에는 올리지 않는다.

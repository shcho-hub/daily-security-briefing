# 🛡️ 일일 보안 동향

매일 아침 수집한 침해사고 · 취약점(CVE) · PoC·악용 정황을 카드 형태로 보는 대시보드입니다.
GitHub Pages로 배포되어 정적 페이지로 동작하며, 브리핑 데이터는 날짜별 JSON 파일로 나뉘어 있습니다.

- 서비스 주소: <https://shcho-hub.github.io/daily-security-briefing/>

## 구성

```
index.html            # 대시보드 (디자인·필터·검색·복사·내보내기)
data/index.json       # 브리핑 날짜 목록 (최신순)
data/YYYY-MM-DD.json  # 해당 날짜의 브리핑 항목 배열
```

페이지를 열면 `data/index.json`을 먼저 불러와 날짜 선택 목록을 만들고,
가장 최근 날짜의 `data/YYYY-MM-DD.json`을 읽어 카드를 그립니다.
날짜 선택에서 **모든 날짜**를 고르면 모든 날짜 파일을 함께 불러와 표시합니다.
(브라우저 캐시를 피하려고 요청마다 `?t=<timestamp>`와 `cache: "no-store"`를 사용합니다.)

## 데이터 필드

각 항목은 아래 필드를 가집니다.

| 필드 | 설명 |
| --- | --- |
| `id` | 항목 고유 ID |
| `date` | 브리핑 날짜 (`YYYY-MM-DD`) |
| `category` | `incident`(국내 침해·유출) · `vuln`(취약점·PoC·KISA) · `global`(글로벌·공급망) |
| `severity` | `critical` · `high` · `info` (2026-11-16 이후) · `critical` · `incident` · `advisory` (이전 데이터, 배지 색상) |
| `severityLabel` | 배지에 표시할 문구 (예: `CVSS 9.8 · 긴급`) |
| `pocStatus` | `exploited`(실제 악용) · `poc`(PoC 공개) · `none`(없음/미확인) — 이전 데이터의 `wild` · `yes`도 함께 지원 |
| `pocLabel` | PoC 배지 문구 |
| `title` | 제목 |
| `summary` | 요약 |
| `pocDetail` | PoC·정황 박스 내용 |
| `action` | 실무 대응 박스 내용 |
| `links` | `[{ "label": "...", "url": "..." }]` 참고 링크 |

## 새 날짜 추가하기

1. `data/YYYY-MM-DD.json` 파일을 만들어 항목 배열을 채웁니다.
2. `data/index.json` 맨 앞(최신순)에 `"YYYY-MM-DD"`를 추가합니다.
3. `main` 브랜치에 커밋·푸시하면 GitHub Pages에 몇 분 안에 반영됩니다.

## 기능

- 카테고리 탭(전체 / 국내 침해·유출 / 취약점·PoC·KISA / 글로벌·공급망)과 날짜 필터, 키워드 검색
- 항목별 **복사** 버튼과 **요약 텍스트 복사**(팀즈 등에 붙여넣기용)
- **JSON / 마크다운** 내보내기

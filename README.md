# 블랙리츠 총판 사업안내서

카드결제 총판 사업을 소개하는 슬라이드형 단일 페이지 랜딩사이트입니다. 수수료 정산 모델을 설명하고, 방문자가 직접 수익을 계산해 본 뒤 미팅을 예약할 수 있습니다.

## 주요 기능

- **슬라이드형 사업안내**: 히어로 · 정산 흐름 · 3가지 정산 방식(D0 즉시 · D1 익일 · 재정산) 등을 섹션 단위로 구성
- **수익 시뮬레이터**: 가맹점 월 매출과 총판 수수료율을 입력하면 월/연간 예상 수익을 즉시 계산
- **미팅 예약 캘린더**: 월 단위 달력 + 시간 슬롯(평일 10:00~18:00, 일요일 휴무, 최대 3개월 후까지) 선택
- **실시간 예약 현황**: Cloudflare Worker `/events` API로 이미 예약된 시간대를 조회해 표시
- **예약 접수 처리**: Worker `/book` API가 중복 예약 체크, KV 저장, Google Calendar 등록, 텔레그램 알림을 담당
- **신청서 + 첨부파일 전송**: Formspree로 신청 정보와 첨부서류(신분증/통장/사업자등록증)를 이메일 전송

## 기술 스택

- 정적 단일 HTML/CSS/JavaScript (의존성 없음, 빌드 불필요)
- Pretendard 웹폰트 (Google Fonts)
- Cloudflare Worker (예약 API: 중복 체크 · KV 저장 · 캘린더 · 텔레그램)
- Google Calendar (예약 일정 등록)
- Telegram (예약 알림)
- Formspree (신청서 이메일 전송)
- GitHub Pages + GitHub Actions(Jekyll) 자동 배포

## 로컬 실행

별도 빌드 과정이 없습니다. 저장소를 클론한 뒤 `index.html`을 브라우저로 열면 됩니다.

```bash
git clone https://github.com/x77xdavid-prog/blackreits.git
cd blackreits
# index.html 을 브라우저로 열기
```

예약 캘린더/접수 기능은 Cloudflare Worker API에 연결되어 동작합니다. Worker 엔드포인트는 `index.html`의 `WORKER_URL` 상수로 지정됩니다.

## 배포

`main` 브랜치에 push하면 `.github/workflows/jekyll-gh-pages.yml` 워크플로가 GitHub Pages로 자동 배포합니다.

## 라이선스

[MIT License](LICENSE)

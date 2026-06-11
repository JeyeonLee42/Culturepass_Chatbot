# 청년문화예술패스 AI 오마카세 플래너

청년문화예술패스 적용 가능 공연 데이터를 기반으로 사용자의 예산, 관람 성향, 관람 빈도, 선호 분야를 반영해 연말까지의 문화생활 계획을 제안하는 정적 웹 MVP입니다.

## 배포 기준

배포 기준 파일은 레포 루트의 아래 3개 파일로 통일합니다.

```text
index.html
culture_db.js
README.md
netlify/functions/llm.js
```

이전에 사용하던 `github_repo_files`, `github_repo_files1` 폴더는 더 이상 배포 기준으로 사용하지 않습니다.

Netlify 연결 시:

- Build command: 비워둠
- Publish directory: `/` 또는 비워둠
- 최종 HTML 파일: 레포 루트의 `index.html`
- LLM API Key: Netlify 환경변수 `LLM_API_KEY`에 등록

선택 환경변수:

- `LLM_MODEL`: 사용할 LLM 모델명
- `LLM_API_URL`: OpenAI 호환 Chat Completions 엔드포인트를 별도로 사용할 경우 지정

## 현재 구현

- AI 오마카세 연간 관람 계획
- 월 단위 관람 추천
- 장바구니 관리
- 예산 관리
- Google Calendar URL 기반 캘린더 메모 등록
- 티켓팅 알림 직접 설정
- 티켓팅 알림 ICS 다운로드
- 작품 추천 챗봇 floating 패널
- localStorage 기반 입력값, 장바구니, 오마카세 플랜 저장/복원
- Netlify Functions 기반 LLM 자연어 조건 해석
- LLM 조건 해석 실패 시 rule-based parser fallback

## 기능 방향

AI 오마카세 플래너는 공연을 정확한 날짜와 회차까지 확정하는 기능이 아니라, 남은 지원금 안에서 어떤 달에 어떤 작품을 보면 좋을지 제안하는 월 단위 관람 계획 기능입니다.

하루짜리 공연은 공연 기간을 참고 정보로 보여줄 수 있지만, 장기 공연/전시는 추천 월 중심으로 표시합니다. 최종 관람일, 회차, 좌석, 잔여석은 예매처에서 사용자가 확정해야 합니다.

티켓팅 알림은 자동 날짜 기반 기능이 아니라, 사용자가 예매처에서 확인한 티켓팅 날짜와 시간을 직접 입력해 캘린더 알림으로 등록하는 보조 기능입니다.

LLM은 사용자의 자연어 입력을 예산, 분야, 선호 월, 회피 조건 같은 추천 조건으로 구조화하는 역할만 합니다. 실제 공연 추천과 점수 계산은 브라우저에서 로드한 `culture_db.js`와 기존 rule-based scoring 로직을 사용합니다.

## 현재 한계

- `ticketOpenDate` 필드는 있으나 실제 값이 없어 자동 티켓팅 알림은 불가
- 실제 관람일 자동 추천 기능 없음
- 회차별 공연 시간과 실제 관람 가능 시간은 데이터에 없음
- 사용자가 예매 시 최종 관람일 결정
- 잔여석, 좌석별 실시간 상태, 예매 오픈 시각은 데이터에 없음
- Google Calendar API 직접 연동은 아직 미구현
- Google Calendar URL 방식에서는 reminder override를 자동 설정하기 어려워, 알림 시점 자체를 별도 캘린더 이벤트로 생성함
- LLM은 조건 해석 용도이며, 공연 추천 자체는 rule-based scoring 기반
- API key는 프론트엔드에 포함하지 않고 Netlify 환경변수로 관리해야 함

## 향후 확장

- 예매처 상세 API/크롤링 고도화를 통한 `ticketOpenDate` 자동 수집
- Google Calendar API 직접 연동을 통한 자동 일정 등록 및 reminder 설정
- 회차별 공연 시간, 잔여석, 예매 오픈일 실시간 반영
- 예매처별 데이터 신뢰도 점검 및 필드 표준화

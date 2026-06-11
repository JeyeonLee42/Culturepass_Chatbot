# 청년문화예술패스 AI 오마카세 플래너

청년문화예술패스 적용 가능 공연 데이터를 기반으로 사용자의 예산, 관람 성향, 관람 빈도, 선호 분야를 반영해 연말까지의 문화생활 계획을 추천하는 정적 웹 MVP입니다.

## 구성 파일

- `index.html`: 오마카세 플래너, 추천 챗봇, 장바구니, 연간 스케줄러 UI
- `culture_db.js`: 서울 공연 DB 및 좌석별 가격 데이터
- `README.md`: 프로젝트 설명 문서

## 주요 기능

- AI 오마카세 연간 관람 플랜 생성
- 예산 슬라이더 및 숫자 입력 동기화
- 관람 성향, 빈도, 선호 분야, 분위기 기반 Rule-Based 추천
- 시험기간 및 특정 월 회피 조건 반영
- 작품 추천 챗봇 floating 패널
- 장바구니 담기 및 예산 계산
- 연간 스케줄러 반영
- ICS 캘린더 저장

## 배포 방법

이 저장소는 별도 빌드 과정이 없는 정적 웹사이트입니다.

Netlify, Vercel, GitHub Pages 등에 아래 파일을 루트 경로로 업로드하면 됩니다.

```text
index.html
culture_db.js
README.md
```

Netlify 연결 시:

- Build command: 비워둠
- Publish directory: `/` 또는 비워둠

## 현재 범위

- 서울 공연 데이터 기반 MVP
- 실제 LLM API 미연동
- 사용자별 저장 기능 미구현
- Google Calendar 직접 API 연동 전 단계로 ICS 저장 방식 사용


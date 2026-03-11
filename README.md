# 📊 CallScore — DJU 성적 조회 시각화 서비스

> 대전대학교 포털에서 성적 데이터를 자동으로 수집하고, 학기별 도넛 차트로 시각화하는 웹 서비스

<br>

## 🧩 핵심 기능

- **자동 로그인 & 크롤링** — Selenium으로 대전대 포털에 자동 로그인 후 전체 성적 파싱
- **학기별 성적 시각화** — Chart.js 도넛 차트로 등급 분포 시각화
- **비동기 처리** — Celery + 로딩 페이지로 크롤링 중 UI 블로킹 방지
- **개인정보 미보관** — 성적 조회 완료 후 세션 데이터 즉시 삭제

<br>

## 🛠 기술 스택

| 분류 | 기술 |
|---|---|
| Backend | Python, Django |
| Scraping | Selenium, BeautifulSoup4, lxml |
| Async | Celery |
| Frontend | Bootstrap 5, Chart.js, jQuery |
| Data | Session 기반 임시 저장 |

<br>

## 🔄 서비스 플로우

```
[로그인 페이지] → 학번 / 비밀번호 입력
      ↓
[로딩 페이지] → Ajax 요청으로 Selenium 크롤링 비동기 실행
      ↓
대전대 포털 자동 로그인 → 통합정보시스템 → 전체성적조회 파싱
      ↓
[성적 조회 페이지] → 학기별 도넛 차트 + 성적표 테이블 표시
```

<br>

## ⚡ 실행 방법

```bash
# 의존성 설치
pip install -r requirements.txt

# Django 마이그레이션
python manage.py migrate

# Celery 워커 실행 (별도 터미널)
celery -A config worker --loglevel=info

# 개발 서버 실행
python manage.py runserver
```

> **Note** Chrome 버전에 맞는 ChromeDriver가 필요합니다.

<br>

## 📁 프로젝트 구조

```
call-score/
├── config/          # Django 프로젝트 설정 (URLs, Views, Celery)
├── callscore/       # 성적 조회 앱
├── module/
│   ├── getScore.py         # Selenium 크롤링 핵심 로직
│   └── processingScore.py  # 차트용 데이터 가공
├── templates/       # HTML 템플릿 (login, loading, viewScores)
├── static/          # CSS, JS, 이미지
├── Prototype/       # 초기 프로토타입 스크립트
└── requirements.txt
```

<br>

---

<p align="right">© 2023 DJU 정보보안학과 20201515</p>

# Internship Project: 채용 공고 분석 및 데이터 크롤링

> 📍 본 프로젝트는 **(주)천재교육 인턴십** 기간 중 진행된 **팀 프로젝트**이며,  
> 이 레포지토리에는 공동 구현 코드가 포함되어 있습니다.  
> 아래 명시된 항목은 제가 **직접 구현하거나 주도적으로 개발한 부분**입니다.

---

## 🔧 사용 기술 스택

- Python (requests, BeautifulSoup, Selenium)
- MySQL
- Linux Shell Script (자동화)
- Git / GitHub
- AWS EC2, AWS SES, AWS Dashboard

---

## 📌 주요 기여 및 설명

### 1. **wanted_crawling.py**
- 원티드 채용공고 페이지 구조를 분석하고 크롤링
- BeautifulSoup, Selenium 기반으로 데이터 정제 및 저장 로직 구현
- 크롤링 주기는 Linux `cron`과 연계하여 자동 실행

### 2. **Job_posting.py**
- 수신거부 처리 로직 개발
- DB에서 수신거부 사용자 목록을 조회하여 메일 전송 대상에서 제외하는 조건 추가

### 3. **run_wanted.sh**
- Linux 자동화 스크립트
- `wanted_crawling.py` 주기 실행을 위한 `.sh` 스크립트 작성 및 테스트

---

## 🧠 핵심 목표

- 맞춤형 채용공고 수집 및 메일 전송 자동화
- 크롤링 → 저장 → 전송까지 전체 흐름의 일부를 주도적으로 구성

---

## 🔒 참고 사항

> 해당 프로젝트는 팀 공동 소유이며,  
> 위 명시된 코드는 본인이 단독 또는 주도적으로 작성한 내용입니다.  
> 개인정보나 민감한 설정 정보는 포함되어 있지 않습니다.




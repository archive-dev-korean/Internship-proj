# 맞춤형 채용 공고 제공 프로젝트
## 개요
- Python 기반 채용 공고 수집/필터링 자동화 서비스를 구축하고, AWS(EC2, SES, CloudWatch) 환경에서 운영하여 KDT 수강생에게 맞춤형 채용 공고를 이메일로 발송
- **해당 서비스에서 담당한 부분만 발췌**
## 일정
- 2024.09 ~ 2024.11
## 사용 기술 및 개발 환경
- Language : Python, SQL
- DB : MySQL(채용 공고 저장), LMS DB 연동(수신자/과정 데이터 조회)
- Infrastructure : AWS EC2, SES(Configuration Set 기반 발송 추적), Linux cron
- Monitoring : SES 발송 결과 추적 체계(Configuration Set)를 활용
- Framwork/Platform : Docker
- Tool : Linux VM, Git, Jira, Slack
## 내용
### 개발 배경
- KDT 운영 절차상 수료 후 6개월간 취업 지원 서비스 필수
- 내부 직원들 취업정보 제공에 대한 채용공고 수집 반복 작업 발생
- 업무 자동화를 통해 업무 효율성 증대 목적
### 구현 기능
- Selenium/BeautifulSoup 기반 채용 공고 수집 및 정제 로직 구현
- 공고 마감 여부 확인 작업을 asyncio로 동시 처리하여 검증 시간 단축 (동시 실행 수 제한 적용)
- 수신 거부(Google Form/Sheet) 기반 차단 로직을 발송 직전 조회로 즉시 반영, DB는 주기 배치로 동기화
- SES 메일 발송 시 Configuration Set을 지정해 발송 로그/추적 체계에 맞춰 애플리케이션을 연동

### 크롤링 전략
- 해당 사이트 담당자에게 크롤링 날짜/시간 관련 이메일 발송 후 결정
  - 원티드 : 매 수,토 요일 오전 1시 기준 공고 대략 20개씩 크롤링 진행
### 메일 발송 조건

| 구분 | 조건 | 처리 |
|------|------|------|
| 과정 기간 | 시작일 + 4.5개월 ~ 종료일 + 6개월 이전 | 발송 |
| 과정 기간 | 위 범위 외 | 발송 제외 |
| 학생 상태 | 교육중 / 수료 / 조기수료 | 발송 |
| 학생 상태 | 취업 / 중도포기 / 수강철회 | 발송 제외 |
| 공고 검증 | 마감 여부 확인 (사이트별 10개 샘플) | 제외 처리 |

### 수신 거부 전략
- 수신 거부 요청은 실시간으로 Google Sheet에 반영되며, 메일 발송 직전에 Sheet를 조회하여 즉시 반영되도록 처리
- DB 동기화는 운영 효율을 위해 주 1회 배치로 갱신

### 운영 환경
- EC2(Linux)에서 cron 기반 배치 실행
- 실행 로그 기반으로 장애 원인 추적
- SES를 통해 대량 메일 발송 처리

## 실행 흐름
1) cron → `run_wanted.sh` 실행  
2) `wanted_crawling.py` 크롤링 및 DB 저장  
3) `Job_posting.py` 수신거부/조건 필터링 후 SES 발송

### 공고명 키워드
<img width="783" height="840" alt="image" src="https://github.com/user-attachments/assets/a7dcb453-823c-4f5b-8030-9cd04c55a0ca" />


### 제외 키워드
<img width="774" height="390" alt="image" src="https://github.com/user-attachments/assets/45492448-661b-436a-bbd5-7cc295c6eec8" />



## 성과
- 연간 약 1100만원 인력 비용 절감, 수집 부터  발송 전 과정 자동화 구축 및 운영 경험
  - 시급 2만원 x 2시간(정보 수집 및 상담 시간) = 4만원 x 5명 x 52주 = 대략 1100만원
## 참고 사항
> 해당 프로젝트는 팀 공동 소유이며, 
> 개인정보나 민감한 회사 내부 설정 정보(인프라 구조, 시퀀스 등)는 포함되어 있지 않습니다.

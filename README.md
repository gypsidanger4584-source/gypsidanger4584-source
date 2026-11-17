# [작성 필요] 포트폴리오

> [작성 필요: 한 줄 소개]

## Contact
- Email: [gypsidanger4584@gmail.com]
- Blog: [작성 필요]
- Github: https://github.com/gypsidanger4584-source

## Projects

### 1. EvCharge (projectelectric)

| 항목 | 내용 |
|---|---|
| 소개 | 전기차 충전기 예약 서비스. 동시 예약에서 이중 예약을 막고, 비관적 락과 Redisson 분산 락을 부하 테스트로 비교한 백엔드 프로젝트 |
| 개발 기간 | [작성 필요] |
| 개발 인원 / 역할 | [작성 필요] |
| 기술 스택 | Java 17 / Spring Boot 4 / Spring Security / Spring Data JPA / PostgreSQL 16 / Redis 7 (Redisson) / ShedLock / Docker / k6 / Prometheus, Grafana / GitHub Actions |
| 주요 내용 | - 충전기당 PENDING 예약이 최대 20건까지 쌓이던 이중 예약을 락 후 재조회, 커밋 뒤 unlock, partial unique로 막아 최대 1건으로 맞췄습니다.<br>- 같은 조건(VU 50, 충전기 50기, 단일 인스턴스)에서 마지막 성공까지 걸린 시간은 PESSIMISTIC 4.197초, REDISSON 8.776초였습니다. |
| 링크 | [프로젝트 Repository](https://github.com/gypsidanger4584-source/projectelectric) / [부하 테스트 보고서](https://github.com/gypsidanger4584-source/projectelectric/blob/main/docs/loadtest-report.md) |
| 회고록 | [작성 필요] |

### 2. 연성 커넥트 (project-connect)

| 항목 | 내용 |
|---|---|
| 소개 | 캠퍼스 생활용 Android 앱. 게시판, 시간표, 캠퍼스 지도, 스터디방, 학식 랜덤 매칭, AI 채팅 화면을 구현했습니다. |
| 개발 기간 | 2025.04 ~ 2025.11 |
| 개발 인원 / 역할 | 4인 팀 / 시간표, 로그인, 학식 랜덤 매칭 채팅, 관리자 기능 구현, 스터디 채팅방 아이디어 기획 |
| 기술 스택 | Java 17 / Android (minSdk 31, targetSdk 35) / Firebase Auth, Firestore / Room / WorkManager / Retrofit, OkHttp / Glide / Biometric |
| 주요 내용 | - 시간표: Room DB에 강의를 저장하고 WorkManager 주기 작업으로 다음 수업 알림을 띄웠습니다.<br>- 학식 랜덤 매칭: Firestore 대기열(`waiting`)과 트랜잭션으로 짝을 맺고, 1분 안에 매칭되지 않으면 실패 화면으로 이동하도록 했습니다. 대기열 조회에는 복합 색인(status, createdAt)을 설계했습니다.<br>- 로그인: 학번으로 이메일을 조회해 Firebase Auth로 로그인하고, 지문 인증 로그인을 붙였습니다.<br>- 관리자: 사용자 문서의 `role` 값으로 공지사항 작성과 공지 수정·삭제 권한을 나눴습니다.<br>- TFLite 비속어 필터를 구현했으나 문제가 생겨 제거했습니다. [작성 필요: 제거 사유] |
| 링크 | [프로젝트 Repository](https://github.com/gypsidanger4584-source/project-connect) |
| 회고록 | [작성 필요] |

### 3. my-grass (알고리즘 풀이)

| 항목 | 내용 |
|---|---|
| 소개 | 프로그래머스 Java 풀이와 Oracle SQL 풀이 저장소 |
| 풀이 현황 | Java Lv.0 204개, Lv.1 79개, Lv.2 16개 / Oracle SQL 9개 |
| 기술 스택 | Java / Oracle SQL / BaekjoonHub 자동 커밋 |
| 링크 | [Repository](https://github.com/gypsidanger4584-source/my-grass) |

***

# [유대웅] 포트폴리오

> [기존 시스템의 안정성은 지키고, 새로운 변화에는 유연한 개발자]

## Contact
- Email: [gypsidanger4584@gmail.com]
- Github: https://github.com/gypsidanger4584-source

## Projects

### 1. EvCharge (projectelectric)

| 항목 | 내용 |
|---|---|
| 소개 | 전기차 충전기 예약 서비스. 동시 예약에서 이중 예약을 막고, 비관적 락과 Redisson 분산 락을 부하 테스트로 비교한 백엔드 프로젝트 |
| 개발 기간 | 2026.08 ~ 2026.10 |
| 개발 인원 / 역할 | 개인 프로젝트 |
| 담당 업무 | 설계부터 구현, 부하 테스트까지 전부 담당. 충전기 예약 API, 락 전략(비관적 락, Redisson) 구현과 전환, 만료 예약 스케줄러(ShedLock), Redis 기반 로그인 시도 제한, k6 부하 테스트, Prometheus/Grafana 모니터링, GitHub Actions CI |
| 기술 스택 | Java 17 / Spring Boot 4 / Spring Security / Spring Data JPA / PostgreSQL 16 / Redis 7 (Redisson) / ShedLock / Docker / k6 / Prometheus, Grafana / GitHub Actions |
| 주요 내용 | - 충전기당 PENDING 예약이 최대 20건까지 쌓이던 이중 예약을 락 후 재조회, 커밋 뒤 unlock, partial unique로 막아 최대 1건으로 맞췄습니다.<br>- 같은 조건(VU 50, 충전기 50기, 단일 인스턴스)에서 마지막 성공까지 걸린 시간은 PESSIMISTIC 4.197초, REDISSON 8.776초였습니다. 멀티 인스턴스는 아직 측정하지 않았습니다. |
| 트러블슈팅 | - **이중 예약:** k6 응답은 50건 모두 성공이었지만 DB에는 충전기당 PENDING이 최대 20건이었습니다. 원인은 긴 트랜잭션에서 읽은 낡은 상태로 검증한 것, Redisson unlock이 DB 커밋보다 먼저 실행될 수 있던 것, DB에 제약이 없던 것이었습니다. 락 후 재조회, 커밋 뒤 unlock, partial unique index로 해결했습니다. (보고서 3장)<br>- **커넥션 풀 고갈:** 409 폴백을 추가하자 50건이 전부 실패하고 Hikari 타임아웃이 났습니다. 바깥 트랜잭션이 커넥션을 잡은 채 `REQUIRES_NEW`를 반복한 것이 원인이어서, 오케스트레이션을 `NOT_SUPPORTED`로 분리하고 풀 설정을 보강했습니다. (보고서 5장)<br>- **취소와 만료의 충돌:** 코드를 점검하다가, 취소가 읽기와 flush 사이에 만료와 겹치면 상태를 덮어쓸 수 있다는 것을 발견했습니다. 실제로 재현하지는 못했고, 취소를 `status = PENDING` 조건부 UPDATE(CAS)로 바꿔 0건이면 409를 반환하도록 했습니다. |
| 테스트 · 운영 | - k6 부하 테스트와 Prometheus/Grafana 대시보드로 락 전략별 처리 시간을 측정했습니다.<br>- 취소 CAS 단위 테스트를 작성했고, GitHub Actions가 Postgres·Redis 서비스 컨테이너를 띄워 빌드와 테스트를 실행합니다. |
| 링크 | [프로젝트 Repository](https://github.com/gypsidanger4584-source/projectelectric) / [부하 테스트 보고서](https://github.com/gypsidanger4584-source/projectelectric/blob/main/docs/loadtest-report.md) |

### 2. 연성 커넥트 (project-connect)

| 항목 | 내용 |
|---|---|
| 소개 | 캠퍼스 생활용 Android 앱. 게시판, 시간표, 캠퍼스 지도, 스터디방, 학식 랜덤 매칭, AI 채팅 화면을 구현했습니다. |
| 개발 기간 | 2025.04 ~ 2025.11 |
| 개발 인원 / 역할 | 4인 팀 / 시간표, 로그인, 학식 랜덤 매칭 채팅, 관리자 기능 구현, 스터디 채팅방 아이디어 기획 |
| 기술 스택 | Java 17 / Android (minSdk 31, targetSdk 35) / Firebase Auth, Firestore / Room / WorkManager / Retrofit, OkHttp / Glide / Biometric |
| 주요 내용 | - 시간표: Room DB에 강의를 저장하고 WorkManager 주기 작업으로 다음 수업 알림을 띄웠습니다.<br>- 학식 랜덤 매칭: Firestore 대기열(`waiting`)과 트랜잭션으로 짝을 맺고, 1분 안에 매칭되지 않으면 실패 화면으로 이동하도록 했습니다. 대기열 조회에는 복합 색인(status, createdAt)을 설계했습니다.<br>- 로그인: 학번으로 이메일을 조회해 Firebase Auth로 로그인하고, 지문 인증 로그인을 붙였습니다.<br>- 관리자: 사용자 문서의 `role` 값으로 공지사항 작성과 공지 수정·삭제 권한을 나눴습니다. |
| 보안 개선 (2026.11) | 자동 로그인 비밀번호를 암호화 저장소로 옮기고, OpenAI 키를 소스에서 분리했으며, 앱 내 관리자 코드 입력 방식을 없앴습니다. Firestore 보안 규칙에서 `role` 변경을 막았고, 이 규칙은 AI 도움을 받아 작성했습니다. |
| 링크 | [프로젝트 Repository](https://github.com/gypsidanger4584-source/project-connect) |

***

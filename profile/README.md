# watchbox-net

## 📃 개요

| 항목     | 상세 |
| ------ | ----------------------------------------------------------- |
| 소개     | 영화·시리즈 시청 상태와 취향을 간편하게 기록하고  사람들과 공유하는 서비스|
| 기간     | 26년 01월 ~ 지속 |
| 인원     | 개인 |
| 서비스 링크 | [Web](https://watch-box.net) |

## 📜 주요 기능

| 기능         | 상세                                                              |
| ---------- | --------------------------------------------------------------- |
| 홈 응답 개선    | TMDB Redis read-through 캐시, HTTP/2 커넥션 풀, 기동·주기 캐시 워밍           |
| 알림 유실 방지   | 트랜잭션 아웃박스 + Kafka 발행·소비, 재시도·멱등 처리, 로컬/Kafka 런타임 스위치            |
| 실시간 알림     | SSE, 커밋 후 비동기 fan-out, 하트비트·재연결·catch-up                        |
| 전달 계측      | SSE·메일 채널별 성공/실패/스킵 카운터, 실패 주입으로 도입 전후 도착률 비교                   |
| 무한스크롤      | QueryDSL 커서(keyset) 페이지네이션, 복합키 Base64 커서, 혼합 정렬                |
| N+1 제거     | 다형(movie/tv/person) fetch join, IN 배치, 2-phase 집계 분리            |
| 리프레시 토큰 회전 | Redis 세션, memberId 락(SETNX+Lua CAS), grace window, 재사용 감지       |
| 관측         | OpenTelemetry OTLP, Micrometer 커스텀 지표, Grafana·Tempo, Pyroscope |

## 🧭 IA (Information Architecture)
<img width="1656" height="881" alt="image" src="https://github.com/user-attachments/assets/312fa9bc-c8a0-4ad7-baea-dcd769c9658b" />

## ## ⚙️ 기술 스택
### Frontend
| 구분 | 기술 |
| --- | --- |
| Language | TypeScript 5 |
| Framework | Next.js 16 (App Router) |
| UI | React 19, Tailwind CSS 4 |
| Data Fetching | TanStack Query 5, Axios |
| Realtime | SSE (EventSource) |

### Backend
| 구분            | 기술                                        |
| ------------- | ----------------------------------------- |
| Language      | Java 21 (LTS)                             |
| Framework     | Spring Boot 3.5.7, Spring Web MVC         |
| Build         | Gradle                                    |
| ORM           | Spring Data JPA (Hibernate), QueryDSL 5.0 |
| Database      | MySQL 8.4                                 |
| Cache / Store | Redis 7.2 (Spring Data Redis)             |
| Messaging     | Apache Kafka (Confluent 7.6, KRaft)       |
| Security      | Spring Security, OAuth 2.0, JWT           |
| HTTP Client   | Spring WebClient                          |
| Realtime      | SSE (SseEmitter)                          |
| Push          | Web Push (VAPID)                          |
| Mail          | Spring Boot Starter Mail, AWS SES (SMTP)  |
| API Docs      | springdoc-openapi (Swagger UI)            |

### Cloud & External Services
| 서비스 | 용도 |
| --- | --- |
| AWS EC2 | 애플리케이션 서버 (t4g, ARM64 Graviton) |
| AWS S3 | 이미지·파일 저장 |
| AWS Route 53 | 도메인 · DNS |
| AWS SES | 메일 발송 |
| TMDB API | 영화 · TV · 인물 데이터 |

### Infra & DevOps
| 구분 | 기술 |
| --- | --- |
| Container | Docker, Docker Compose |
| CI/CD | GitHub Actions (self-hosted runner) |
| Web Server | Nginx |
| SSL | Certbot (Let's Encrypt) |

### Observability
| 구분 | 기술 |
| --- | --- |
| Instrumentation | OpenTelemetry (Spring Boot Starter · Web SDK), Micrometer |
| Pipeline | OpenTelemetry Collector |
| Trace | Tempo 2.9 |
| Metric | Prometheus |
| Log | Loki |
| Profile | Pyroscope |
| Dashboard | Grafana |
| Exporter | mysqld-exporter, redis-exporter |

## 🏛️ System Architecture
<img width="1751" height="943" alt="image" src="https://github.com/user-attachments/assets/4ed7b198-7298-4cac-a6a2-0fbc3f94b6df" />

## 📊 ERD
<img width="2238" height="2040" alt="image" src="https://github.com/user-attachments/assets/d89d1368-1845-4de3-b575-081cdb4844ab" />


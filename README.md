# 동아리 통합 플랫폼 동아리움 

[서비스 링크](https://dongarium.co.kr)
## 개발 환경
### Language 
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
### Framework & Runtime
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)
### Database
![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/redis-%23DD0031.svg?style=for-the-badge&logo=redis&logoColor=white)
### Infra & Messaging
![AWS S3](https://img.shields.io/badge/AWS%20S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white)
### DevOps & CI/CD
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

<hr>

## Key Dependencies and Features

### 1. Monolithic Architecture
- 단일 애플리케이션 내에서 모든 도메인 로직을 처리하는 모놀리식 구조
- 인증/회원, 동아리, 게시판, 댓글, 파일 관리 등의 기능을 모듈화하여 관리
- Spring Boot 기반의 REST API 서버로 구성

### 2. OAuth2 & JWT Authentication
- Kakao OAuth2 로그인을 통한 간편한 소셜 로그인 지원
- JWT(Access Token, Refresh Token) 기반의 무상태(Stateless) 인증 방식 적용
- Spring Security를 활용한 역할 기반 접근 제어(RBAC) 구현

### 3. Redis Caching & Session Management
- Redis를 활용하여 Refresh Token 저장 및 관리
- 이메일 인증 코드 등의 임시 데이터 캐싱 처리
- 빠른 데이터 조회를 위한 캐시 레이어로 활용

### 4. AWS S3 File Upload
- 동아리 활동 사진, 게시글 첨부 파일 등을 AWS S3에 안전하게 저장
- Presigned URL 또는 직접 업로드 방식을 통해 효율적인 파일 관리 지원

### 5. Discord Webhook Logging
- 서버 에러 및 주요 이벤트를 Discord Webhook으로 실시간 알림 전송
- Logback Appender를 활용하여 비동기 로그 전송 구현

<hr>

## 아키텍처
### 소프트웨어 아키텍처

![소프트웨어 아키텍처](https://private-user-images.githubusercontent.com/138632648/531698557-ddde2cfa-3ded-472f-876b-929153f18d4c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njc1MDU1MzQsIm5iZiI6MTc2NzUwNTIzNCwicGF0aCI6Ii8xMzg2MzI2NDgvNTMxNjk4NTU3LWRkZGUyY2ZhLTNkZWQtNDcyZi04NzZiLTkyOTE1M2YxOGQ0Yy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTA0JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEwNFQwNTQwMzRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wNjlmZmFiYzdjYmE5ZmNiMmM3ZWQxYTgwNWY4OWNlM2Y2ZTYzOTUzNTE1ZmRjZTQ0OTkxODE0YzZiYTM2YjRkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.a2v0f468x5TIGXw1vKtZlRCDINE4ZNCOQ7x_wOE_e3A)
본 시스템은 대학 동아리 관리 및 커뮤니티 기능을 제공하는 모놀리식 서비스 구조로 설계되어 있습니다. <br>
Spring Boot 프레임워크를 기반으로 하며, MySQL을 주 데이터베이스로 사용하고 Redis를 캐시 및 세션 저장소로 활용합니다. <br>
사용자 인증은 OAuth2(Kakao) 및 JWT를 통해 이루어지며, 파일 저장은 AWS S3를 이용합니다. <br>
전체 시스템은 Docker Compose를 통해 컨테이너화되어 배포 및 관리가 용이하도록 구성되어 있습니다. <br>

### ERD
![ERD](https://private-user-images.githubusercontent.com/138632648/531698772-3b38d60f-3404-4550-bff9-881290754925.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njc1MDU4MDMsIm5iZiI6MTc2NzUwNTUwMywicGF0aCI6Ii8xMzg2MzI2NDgvNTMxNjk4NzcyLTNiMzhkNjBmLTM0MDQtNDU1MC1iZmY5LTg4MTI5MDc1NDkyNS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTA0JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEwNFQwNTQ1MDNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05Y2NiOGRlYjZiNjgwOGYzZTg2ODc4MmI5Njc4ZDA3MTY0MGQxNDhmMGIzMTYwYTNlNjIwZmYyMTBkY2JmZWQyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.-LOqeSTquCcfARYTetxXra-o3UZoq9nVUT0HE8DthoY)

| 도메인명               | 설명                                                     |
| ------------------ | ------------------------------------------------------ |
| **Auth & User**    | OAuth2 기반 소셜 로그인 및 JWT 인증 관리, 사용자 기본 정보(학번, 학과 등) 및 권한 관리 |
| **Club**           | 동아리 기본 정보(이름, 소개, 카테고리) 및 활동 이미지 관리, 동아리 멤버(운영진/부원) 및 역할(Role) 관리 |
| **ClubApplyForm**  | 동아리별 맞춤형 지원서 양식 생성 및 관리, 질문(FormQuestion) 및 선택지(TimeSlotOption) 구성 |
| **Application**    | 지원자의 지원서 제출 및 상태(서류/면접/최종) 관리, 지원서 답변(Answer) 저장 및 평가 프로세스 처리 |
| **Notice**         | 동아리 내 공지사항 게시글 작성 및 조회, 댓글(Comment) 기능을 통한 커뮤니케이션 지원 |
| **ClubReview**     | 동아리 활동 후기 및 평점 관리, 사용자 피드백 수집 기능 제공 |

<br>

### 시스템 아키텍처
![시스템 아키텍처](https://private-user-images.githubusercontent.com/138632648/531698815-7760cf10-0afc-44d2-a734-586e8bba6980.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Njc1MDU4NzQsIm5iZiI6MTc2NzUwNTU3NCwicGF0aCI6Ii8xMzg2MzI2NDgvNTMxNjk4ODE1LTc3NjBjZjEwLTBhZmMtNDRkMi1hNzM0LTU4NmU4YmJhNjk4MC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMTA0JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDEwNFQwNTQ2MTRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1mZjgwZTY2NjgwMmZmZTk4MGQ5ZWMyZDJiNzA1Y2Q4NjY1ZTk1MTY2NzgxZTA2M2I1NzRiZDg5OTA1Yzk1YzdmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.0c39javhgOrasR4lu7R00L1LdqM1TD7tZ5Cf6k5Ztp8)

단일 Spring Boot 애플리케이션이 모든 비즈니스 로직을 처리하며, MySQL과 Redis, AWS S3와 연동됩니다. <br>
Docker Compose를 사용하여 애플리케이션과 데이터베이스, Redis를 통합 관리합니다. <br>

**EC2 + Docker 컨테이너 기반 구성**  

개발·운영 환경 차이와 서버 구성 변경으로 인한 배포 오류 가능성을 문제로 인식하여, 단일 EC2 인스턴스 위에 Spring Boot, MySQL, Redis, Nginx를 Docker 컨테이너로 분리 구성함으로써 실행 환경을 표준화하고 유지보수성과 확장성을 함께 확보했다.

**Nginx Reverse Proxy 도입**

애플리케이션 서버가 HTTPS 처리와 라우팅까지 담당할 경우 운영 복잡도가 증가할 수 있다고 판단하여, Nginx를 Reverse Proxy로 두어 HTTPS 종단 처리와 API 라우팅을 분리함으로써 Spring Boot가 비즈니스 로직에 집중할 수 있는 구조를 만들었다.

**ECR 기반 Docker 이미지 배포**

코드 기반 배포 방식에서는 배포 시점의 실행 환경을 정확히 재현하기 어렵다는 문제가 있어, Docker 이미지를 빌드해 ECR에 저장하는 배포 전략을 도입함으로써 CI/CD 파이프라인의 안정성과 배포 일관성을 확보했다.

**Redis 기반 Refresh Token 관리**

Access Token 만료 시 재로그인이 반복되는 사용자 경험 저하와 토큰 탈취 위험을 해결하기 위해, Refresh Token을 Redis에 저장하고 토큰 재발급 로직을 구현함으로써 재로그인 없이 서비스를 지속할 수 있으면서도 서버 단에서 토큰 무효화가 가능한 보안 구조를 구축했다.


**MySQL + Redis 역할 분리**

인증 및 반복 조회 요청이 증가할 경우 단일 DB 구조에서 성능 병목이 발생할 수 있다고 판단하여, 핵심 데이터는 MySQL에 저장하고 인증·세션 관련 데이터는 Redis에서 처리하도록 역할을 분리함으로써 API 응답 속도를 개선하고 데이터베이스 부하를 효과적으로 분산시켰다.


<br>

## API URI Collection
[Swagger 링크](https://dongarium.co.kr/swagger-ui/index.html)
### Auth  API
| URI                                    | Method | 설명                |
| -------------------------------------- | ------ | ----------------- |
| `/api/auth/kakao/login`                | POST   | 카카오 인가 코드로 로그인/회원가입 |
| `/api/auth/register`                   | POST   | 추가 정보 제출 및 최종 회원가입 |
| `/api/auth/reissue`                    | POST   | Access Token 재발급   |
| `/api/auth/logout`                     | POST   | 서비스 로그아웃          |
| `/api/auth/kakao/logout`               | GET    | 카카오계정과 함께 로그아웃     |

<br>

### Club API
| URI                                    | Method | 설명                |
| -------------------------------------- | ------ | ----------------- |
| `/api/clubs`                           | GET    | 전체 동아리 목록 조회      |
| `/api/clubs`                           | GET    | 카테고리별 동아리 목록 조회 (param: category) |
| `/api/clubs/{clubId}`                  | GET    | 특정 동아리 상세 정보 조회    |
| `/api/clubs/{clubId}`                  | POST   | 특정 동아리 상세 정보 수정    |
| `/api/clubs/{clubId}/images`           | PUT    | 특정 동아리 상세 이미지 수정   |
| `/api/clubs/{clubId}/dashboard`        | GET    | 동아리 대시보드 정보 조회     |
| `/api/clubs/{clubId}/dashboard/applicants` | GET | 동아리 대시보드 지원자 목록 필터링 조회 |

<br>

### Club Apply Form API
| URI                                    | Method | 설명                |
| -------------------------------------- | ------ | ----------------- |
| `/api/clubs/{clubId}/apply`            | GET    | 지원서 양식 조회 (사용자용) |
| `/api/clubs/{clubId}/dashboard/apply-form` | GET | 지원서 양식 조회 (운영진용) |
| `/api/clubs/{clubId}/dashboard/apply-form` | POST | 지원서 양식 저장         |
| `/api/clubs/{clubId}/dashboard/apply-form` | PATCH | 지원서 양식 수정         |

<br>

### Application API
| URI                                    | Method | 설명                |
| -------------------------------------- | ------ | ----------------- |
| `/api/clubs/{clubId}/apply-submit`     | POST   | 지원서 제출            |
| `/api/clubs/{clubId}/applicants/{applicantId}/application` | GET | 지원서 상세 조회 (운영진용) |
| `/api/clubs/{clubId}/applications/{applicationId}/status` | PATCH | 지원서 상태 변경 (운영진용) |
| `/api/clubs/{clubId}/club-apply-form/result` | PATCH | 합/불 처리 및 메시지 전송    |

<br>

### Comment API
| URI                                    | Method | 설명                |
| -------------------------------------- | ------ | ----------------- |
| `/api/applications/{applicationId}/comments` | GET | 특정 지원서의 댓글 조회 |
| `/api/applications/{applicationId}/comments` | POST | 댓글 작성 |
| `/api/applications/{applicationId}/comments/{commentId}` | PATCH | 댓글 수정 |
| `/api/applications/{applicationId}/comments/{commentId}` | DELETE | 댓글 삭제 |

<br>

### Club Review API
| URI                                    | Method | 설명                |
| -------------------------------------- | ------ | ----------------- |
| `/api/clubs/{clubId}/reviews`          | POST   | 동아리 후기 등록       |
| `/api/clubs/{clubId}/reviews`          | GET    | 동아리 후기 조회       |

<br>

### Notice API
| URI                                    | Method | 설명                |
| -------------------------------------- | ------ | ----------------- |
| `/api/notices`                         | GET    | 공지사항 목록 조회        |
| `/api/notices/{noticeId}`              | GET    | 공지사항 상세 조회        |

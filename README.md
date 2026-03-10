# LiveCoder Backend

백준 스타일의 문제 풀이 플랫폼을 목표로 제작한 **Spring Boot 기반 백엔드 프로젝트**입니다.  
사용자 인증, 문제 CRUD 및 채점, 커뮤니티, 친구/쪽지, 알림, 홈 추천, 협업 팀(collab) 기능을 REST API 형태로 구현했습니다.

이 저장소는 팀 프로젝트 기반의 **개인 포트폴리오 정리용 백엔드 레포지토리**이며,  
전체 백엔드 코드를 기준으로 정리하되 **내가 담당한 기능은 따로 명시**했습니다.

---

## 프로젝트 소개

LiveCoder는 단순한 문제 풀이 사이트를 넘어서,  
사용자 간의 소통과 협업까지 고려한 코딩 플랫폼을 목표로 설계한 프로젝트입니다.

주요 흐름은 다음과 같습니다.

- JWT 기반 회원가입 / 로그인 / 인증
- 문제 조회 / 문제 제출 / 채점 / 제출 기록 저장
- 커뮤니티 게시글 / 댓글 / 좋아요 / 공지
- 친구 요청 / 수락 / 삭제 / 쪽지
- 읽지 않은 알림 조회 및 읽음 처리
- 홈 화면 추천 게시글 / 뉴스 / 최근 푼 문제 제공
- 협업 팀 구성 및 협업 코드 구조 설계

---

## 담당 기능

이 프로젝트에서 내가 중점적으로 구현하고 정리한 부분은 다음과 같습니다.

### 내가 맡은 핵심 구현
- **커뮤니티(post) 도메인**
- **홈(home) 도메인**
- **협업(collab) 도메인 구조**
- DB 스키마 리바이즈 및 기능 정의 반영
- API 응답 구조 / 예외 처리 정리
- GitHub 개인 포트폴리오용 백엔드 정리

### 내가 구현한 주요 기능 상세

#### 1. 커뮤니티 기능 (`post`)
- 공지사항 3개 상단 고정 + 일반 게시글 페이징
- 카테고리별 게시글 목록 조회
- 게시글 검색 및 정렬 기능
  - 최신순
  - 오래된순
  - 조회수순
  - 좋아요순
  - 댓글순
- 게시글 상세 조회
- 조회수 증가
- 게시글 작성 / 수정 / 삭제
- 댓글 작성 / 수정 / 삭제
- 대댓글 작성 / 삭제
- 댓글 트리 구조 응답
- 좋아요 / 좋아요 취소
- 관리자 공지 작성
- 첨부파일 업로드 / 다운로드 / 삭제
- 게시글 삭제 시 댓글, 좋아요, 첨부파일 정리 후 삭제

#### 2. 홈 기능 (`home`)
- 조회수 기준 추천 게시글 TOP 5
- 뉴스 최신순 TOP 5
- 사용자의 최근 푼 문제 조회
  - 정답 제출 기준
  - 동일 문제 중복 제거
  - 최신 제출 기준 정렬
- 뉴스 전체 페이징 조회

#### 3. 협업 기능 (`collab`)
- 협업 팀 엔티티 설계
- 협업 팀 멤버 구조 설계
- 원본 코드 / 답글 버전 구조 설계
- 협업 초대 상태 구조 설계
- 문제 연동형 협업 팀 도메인 설계
- 공개/비공개 및 비밀번호 협업방 구조 고려

---

## 전체 기능 구성

### 1. 사용자 기능 (`user`)
- 회원가입
- 로그인 / 로그아웃
- JWT 토큰 기반 인증 상태 확인
- 사용자 조회
- 사용자 정보 수정
- 비밀번호 변경
- 이메일 변경
- 풀이 공개 여부 변경
- 회원 탈퇴
- 닉네임 검색 / 사용자명 검색

### 2. 문제 기능 (`problem`)
- 문제 생성 / 조회 / 수정 / 삭제
- 난이도(Difficulty) 관리
- 문제 상세 조회
- 코드 실행 및 채점
- 제출 기록 저장
- 제출 기록 상세 조회

### 3. 채점 기능 (`judge`)
- Docker 기반 Java 실행 환경 사용
- 샘플 입력/출력 기준 채점
- 컴파일 에러 / 런타임 에러 / 시간 초과 / 메모리 초과 처리
- 실행 시간(ms), 메모리 사용량(KB) 측정
- 세션 기반 임시 채점 결과 저장 후 제출 기록 생성

### 4. 커뮤니티 기능 (`post`)
- 공지 / 일반글 분리
- 댓글 / 대댓글 트리
- 좋아요
- 검색 / 정렬 / 페이징
- 첨부파일 업로드 및 다운로드

### 5. 친구 기능 (`friend`)
- 친구 요청 보내기
- 받은 친구 요청 조회
- 보낸 친구 요청 조회
- 친구 요청 수락 / 거절 / 취소
- 친구 목록 조회
- 친구 삭제
- 친구에게만 쪽지 전송
- 받은 쪽지 / 보낸 쪽지 조회

### 6. 알림 기능 (`notification`)
- 읽지 않은 알림 조회
- 알림 읽음 처리
- 전체 알림 읽음 처리
- 친구 요청 / 쪽지 등에 대한 알림 생성

### 7. 홈 기능 (`home`)
- 추천 게시글
- 뉴스 목록
- 최근 푼 문제 목록

### 8. 협업 기능 (`collab`)
- 협업 팀
- 협업 팀 멤버
- 원본 코드
- 답글 버전 코드
- 초대 상태 관리

---
## 핵심 구현 포인트
1. JWT 기반 인증 구조
로그인 성공 시 JWT 발급
JwtAuthenticationFilter에서 토큰 검증
요청별 userId, username, role 추출
SecurityContext에 인증 정보 등록

2. 커뮤니티 트리 댓글 구조
댓글 / 대댓글을 한 테이블에서 parent_id로 관리
댓글 목록 조회 후 트리 구조로 변환하여 응답
게시글 삭제 시 댓글, 좋아요, 첨부파일 정리 후 삭제

3. 첨부파일 처리
파일 업로드 시 UUID 기반 저장 파일명 생성
원본 파일명 / 저장 파일명 / content type / file size 저장
첨부파일 다운로드 API 제공
작성자만 첨부파일 삭제 가능

4. 홈 추천 데이터 구성
추천 게시글: 조회수 기준 상위 게시글
뉴스: 최신순 정렬
최근 푼 문제: 정답 제출 기준 + 중복 문제 제거 + 최신순
최근 푼 문제는 Native Query를 사용하여 처리

5. Docker 기반 Java 채점
사용자가 제출한 Java 코드를 임시 디렉토리에 저장
Docker 컨테이너에서 javac / java 실행
/usr/bin/time을 활용해 실행 시간 및 메모리 사용량 측정
컴파일 에러 / 런타임 에러 / 시간 초과 / 메모리 초과 분기 처리
---
## API 예시
대표적인 API 예시는 다음과 같습니다.
사용자
POST /users/register
POST /users/login
GET /users/auth-check

문제
GET /problems
GET /problems/{problem_id}
POST /problems/{problem_id}/judge
POST /problems/{problem_id}/submissions

커뮤니티
GET /posts/community
GET /posts/{postId}
POST /posts
POST /posts/{postId}/comments
POST /posts/{postId}/likes
POST /posts/with-files

친구
POST /friends/requests
PUT /friends/requests/{requestId}/accept
POST /friends/msg/{userId}

홈
GET /home
GET /home/news

알림
GET /notifications/unread
PUT /notifications/{notificationId}/read
## 기술 스택

### Backend
- Java 21
- Spring Boot
- Spring Security
- Spring Data JPA
- Gradle
  
실행 환경
JDK 21
Spring Boot
Gradle
MySQL
Docker
IntelliJ IDEA

### Database
- MySQL

### Authentication
- JWT
- BCrypt Password Encoder

### API / Docs
- REST API
- Swagger / SpringDoc OpenAPI

### Judge / Runtime
- Docker
- Java 실행 컨테이너 기반 채점

---

## 프로젝트 구조

실제 코드 기준 패키지 구조는 아래와 같습니다.
```text
src/main/java/com/idea_l/livecoder
├── common
│   ├── CorsConfig
│   ├── GlobalExceptionHandler
│   ├── JwtAuthenticationFilter
│   ├── JwtUtil
│   ├── PasswordConfig
│   ├── SecurityConfig
│   ├── SwaggerConfig
│   └── enum / converter 모음
│
├── user
│   ├── User
│   ├── UserController
│   ├── UserRepository
│   └── UserService
│
├── problem
│   ├── Difficulty
│   ├── ProblemController
│   ├── ProblemService
│   ├── JudgeService
│   ├── Problems
│   ├── docker/java
│   │   ├── Dockerfile
│   │   └── JavaJudgeService
│   └── submissions
│       ├── SubmissionService
│       ├── SubmissionRepository
│       └── Submissions
│
├── post
│   ├── Post
│   ├── Comment
│   ├── PostLike
│   ├── PostAttachment
│   ├── PostController
│   ├── PostService
│   ├── FileStorageService
│   ├── Repository / DTO / Response
│   └── PostExceptionHandler
│
├── friend
│   ├── FriendController
│   ├── FriendService
│   ├── Friendship
│   ├── FriendRequest
│   ├── FriendMessage
│   └── Repository / DTO
│
├── notification
│   ├── Notification
│   ├── NotificationController
│   ├── NotificationService
│   └── NotificationRepository
│
├── home
│   ├── HomeController
│   ├── HomeService
│   ├── News
│   ├── NewsRepository
│   ├── HomeApiResponse
│   └── HomeExceptionHandler
│
└── collab
    ├── CollabTeam
    ├── CollabMember
    ├── CollabCode
    ├── CollabCodeReply
    └── CollabInvite
```
---

## 프로젝트를 통해 배운 점

이 프로젝트를 통해 단순 CRUD 수준을 넘어서,  
실제 서비스형 백엔드를 구성할 때 필요한 여러 요소를 경험할 수 있었습니다.  
특히 아래 부분을 많이 배웠습니다.

- JWT 기반 인증 / 인가 구조
- Spring Security 필터 체인 구성
- 도메인별 패키지 구조 설계
- 게시글 / 댓글 / 좋아요 / 첨부파일 관계 처리
- 친구 / 요청 / 쪽지 / 알림 도메인 분리
- Native Query를 활용한 홈 데이터 구성
- Docker 기반 코드 채점 구조 이해
- DB 스키마와 API 명세를 함께 맞춰 가는 과정
---
## 회고
LiveCoder는 내가 진행한 프로젝트 중에서도
기능 범위가 넓고 도메인 수가 많은 편에 속하는 프로젝트였습니다.
단순히 API 몇 개를 만드는 수준이 아니라,
사용자 / 문제 / 커뮤니티 / 친구 / 알림 / 홈 / 협업 기능을 하나의 서비스 흐름으로 연결해보면서
백엔드 구조를 어떻게 나누고 유지보수 가능하게 설계해야 하는지 많이 고민할 수 있었습니다.
특히 내가 맡았던 커뮤니티, 홈, 협업 구조 설계 부분은
기능 정의와 DB 구조, 응답 형식, 실제 서비스 로직을 함께 맞춰가며 구현했다는 점에서 의미가 컸습니다.

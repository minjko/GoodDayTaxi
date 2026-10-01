# 🚖 GoodDayTaxi

> **차세대 택시 배차 플랫폼 - 더 나은 하루를 위한 택시 서비스**

신뢰성과 편의성을 중시하는 현대적인 택시 배차 시스템입니다. 
마이크로서비스 아키텍처와 이벤트 드리븐 설계로 확장 가능하고 안정적인 서비스를 제공합니다.

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.x-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-17-orange.svg)](https://openjdk.java.net/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-Compose-blue.svg)](https://docs.docker.com/compose/)
[![Kafka](https://img.shields.io/badge/Apache%20Kafka-3.x-red.svg)](https://kafka.apache.org/)

---

## 🎯 프로젝트 소개

### **🌟 서비스 개요**

GoodDayTaxi는 **승객, 기사, 관리자**가 함께 사용하는 통합 택시 배차 플랫폼입니다.

**🎲 핵심 가치**
- **📱 직관적인 UX**: 웹 기반의 심플하고 직관적인 사용자 경험
- **⚡ 실시간 배차**: 이벤트 드리븐 아키텍처로 빠른 배차 처리
- **🔒 안전한 결제**: Toss Payments 연동으로 안전하고 편리한 결제
- **📊 체계적 관리**: 역할 기반 관리 시스템으로 효율적인 운영

### **🏢 서비스 대상**

| 사용자 타입 | 주요 기능 | 특징 |
|------------|----------|------|
| **👤 승객** | 배차 요청, 결제, 이용 내역 조회 | 간편한 택시 호출 및 결제 |
| **🚗 기사** | 배차 수락/거절, 운행 관리, 수익 확인 | 효율적인 운행 관리 |
| **👔 관리자** | 사용자 관리, 통계 조회, 시스템 관리 | 전체 서비스 운영 및 모니터링 |

### **🎯 프로젝트 목표**

1. **🏗 MSA 아키텍처 구현**: 독립적으로 배포 가능한 마이크로서비스 설계
2. **🔄 이벤트 드리븐 설계**: Kafka를 활용한 비동기 처리 및 시스템 간 느슨한 결합
3. **🧪 테스트 자동화**: 단위/통합 테스트를 통한 안정적인 코드 품질
4. **📈 확장 가능한 구조**: 트래픽 증가에 대응할 수 있는 확장 가능한 시스템
5. **🔐 보안 강화**: JWT 기반 인증/인가 및 역할 기반 접근 제어

---

## 🛠 개발환경

### **⚙️ 기술 스택**

#### **Backend**
- **Framework**: Spring Boot 3.5.x, Spring Security, Spring Data JPA
- **Language**: Java 17, Gradle 8.14
- **Database**: PostgreSQL 15
- **Cache**: Redis 7.x
- **Message Queue**: Apache Kafka 3.x, RabbitMQ
- **Authentication**: JWT (JSON Web Token)
- **Documentation**: Swagger/OpenAPI 3

#### **Infrastructure & DevOps**
- **Containerization**: Docker, Docker Compose
- **API Gateway**: Spring Cloud Gateway
- **Monitoring**: Prometheus, Grafana
- **Load Testing**: Artillery, JMeter
- **CI/CD**: GitHub Actions

#### **External APIs**
- **Payment**: Toss Payments API
- **Notification**: Slack API, Push Notification

#### **Development Tools**
- **IDE**: IntelliJ IDEA
- **Version Control**: Git, GitHub
- **API Testing**: Postman, HTTPie
- **Database Tool**: DBeaver, pgAdmin

### **🏗 아키텍처 패턴**

- **마이크로서비스 아키텍처 (MSA)**
- **이벤트 드리븐 아키텍처 (EDA)**
- **Clean Architecture (Hexagonal Architecture)**
- **CQRS (Command Query Responsibility Segregation)**
- **Event Sourcing (부분 적용)**

---

## 🗂 ERD

### **🗄️ 데이터베이스 설계**

**(추후 ERD 이미지로 대체 예정)**

---

## 🚀 프로젝트 실행가이드

### **📋 사전 요구사항**

- **Java 17** 이상
- **Docker & Docker Compose**
- **PostgreSQL 15** (Docker로 실행 권장)
- **Redis** (Docker로 실행 권장)
- **Apache Kafka** (Docker로 실행 권장)

### **🔧 로컬 개발 환경 설정**

#### **1. 프로젝트 클론**
```bash
git clone https://github.com/your-org/GoodDayTaxi.git
cd GoodDayTaxi
```

#### **2. 인프라 서비스 실행**
```bash
# PostgreSQL, Redis, Kafka, Zookeeper 실행
cd infra
docker-compose up -d

# 서비스 상태 확인
docker-compose ps
```

#### **3. 공통 모듈 빌드**
```bash
# 공통 JPA 모듈 빌드 및 로컬 설치
cd common-jpa
./gradlew publishToMavenLocal

# 공통 Core 모듈 빌드 및 로컬 설치  
cd ../common-core
./gradlew publishToMavenLocal
```

#### **4. 각 마이크로서비스 실행**

**🌐 Gateway Service**
```bash
cd gateway
./gradlew bootRun
# 실행 포트: 19091
```

**👤 Account Service**
```bash
cd account-service  
./gradlew bootRun
# 실행 포트: 19092
```

**🚖 Dispatch Service**
```bash
cd dispatch-service
./gradlew bootRun  
# 실행 포트: 19093
```

**🛣 Trip Service**
```bash
cd trip-service
./gradlew bootRun
# 실행 포트: 19094
```

**💳 Payment Service**
```bash
cd payment-service
./gradlew bootRun
# 실행 포트: 19095
```

**📞 Support Service**
```bash
cd support-service
./gradlew bootRun
# 실행 포트: 19096
```

### **🐳 Docker 전체 실행**

```bash
# 전체 서비스 Docker 실행 (예정)
docker-compose up -d
```

---

## 📚 API 명세서

### **🌐 서비스별 API 엔드포인트**

| 서비스 | 포트 | 주요 기능 |
|--------|------|----------|
| **Gateway** | 19091 | 라우팅, 인증, 로드 밸런싱 |
| **Account** | 19092 | 사용자 관리, 인증 |
| **Dispatch** | 19093 | 배차 요청, 배정 |
| **Trip** | 19094 | 운행 관리, 요금 정책 |
| **Payment** | 19095 | 결제, 환불 |
| **Support** | 19096 | 알림, 로깅 |

### **🔑 주요 API 명세**

#### **🔐 Account Service APIs**

<details>
<summary><b>인증 관련 API</b></summary>

**회원가입**
```http
POST /api/v1/auth/signup
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "Password123!",
  "name": "김택시",
  "phoneNumber": "010-1234-5678",
  "role": "PASSENGER|DRIVER|ADMIN|MASTER_ADMIN",
  "vehicleNumber": "12가3456", // 기사만 필수
  "vehicleType": "소나타",     // 기사만 필수
  "vehicleColor": "흰색",      // 기사만 필수
  "slackId": "U1234567"       // 기사/최고관리자만 필수
}
```

**로그인**
```http
POST /api/v1/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "Password123!"
}

Response:
{
  "accessToken": "eyJhbGciOiJIUzI1NiJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiJ9...",
  "userUuid": "550e8400-e29b-41d4-a716-446655440000",
  "role": "PASSENGER"
}
```

**토큰 갱신**
```http
POST /api/v1/auth/refresh
Authorization: Bearer {refreshToken}
```

</details>

<details>
<summary><b>사용자 관리 API</b></summary>

**내 프로필 조회**
```http
GET /api/v1/users/profile
Authorization: Bearer {accessToken}
```

**프로필 수정**
```http
PUT /api/v1/users/profile
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "name": "김수정",
  "phoneNumber": "010-9999-8888"
}
```

**관리자 - 전체 사용자 조회**
```http
GET /api/v1/admin/users
Authorization: Bearer {accessToken}
X-User-Role: ADMIN|MASTER_ADMIN
```

**관리자 - 사용자 상태 변경**
```http
PUT /api/v1/admin/users/{userId}/status
Authorization: Bearer {accessToken}
X-User-Role: MASTER_ADMIN
Content-Type: application/json

{
  "status": "ACTIVE|INACTIVE|DELETED"
}
```

</details>

#### **🚖 Dispatch Service APIs**

<details>
<summary><b>배차 관련 API</b></summary>

**배차 요청 (승객)**
```http
POST /api/v1/dispatches
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "pickupAddress": "서울시 강남구 테헤란로 123",
  "destinationAddress": "서울시 서초구 반포대로 456"
}

Response:
{
  "dispatchId": "550e8400-e29b-41d4-a716-446655440000",
  "status": "REQUESTED",
  "estimatedWaitTime": 300
}
```

**배차 수락 (기사)**
```http
POST /api/v1/dispatches/{dispatchId}/accept
Authorization: Bearer {accessToken}
X-User-Role: DRIVER
```

**배차 거절 (기사)**
```http
POST /api/v1/dispatches/{dispatchId}/reject
Authorization: Bearer {accessToken}
X-User-Role: DRIVER
```

**배차 취소 (승객)**
```http
POST /api/v1/dispatches/{dispatchId}/cancel
Authorization: Bearer {accessToken}
```

**내 배차 목록 조회**
```http
GET /api/v1/dispatches/my
Authorization: Bearer {accessToken}
```

**기사 배차 대기 목록 조회**
```http
GET /api/v1/dispatches/driver/pending
Authorization: Bearer {accessToken}
X-User-Role: DRIVER
```

</details>

#### **🛣 Trip Service APIs**

<details>
<summary><b>운행 관리 API</b></summary>

**운행 시작**
```http
POST /api/v1/trips/{dispatchId}/start
Authorization: Bearer {accessToken}
X-User-Role: DRIVER
```

**운행 종료**
```http
POST /api/v1/trips/{tripId}/end
Authorization: Bearer {accessToken}
X-User-Role: DRIVER
Content-Type: application/json

{
  "endTime": "2024-01-20T10:30:00",
  "totalDistance": 15.5,
  "totalDuration": 25
}
```

**운행 내역 조회**
```http
GET /api/v1/trips/my?page=0&size=10
Authorization: Bearer {accessToken}
```

**요금 정책 조회**
```http
GET /api/v1/fare-policies/current
```

</details>

#### **💳 Payment Service APIs**

<details>
<summary><b>결제 관련 API</b></summary>

**결제 생성**
```http
POST /api/v1/payments
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "tripId": "550e8400-e29b-41d4-a716-446655440000",
  "method": "CARD|CASH",
  "amount": {
    "totalAmount": 15000,
    "currency": "KRW"
  }
}
```

**Toss Payments 결제 승인**
```http
POST /api/v1/payments/toss/confirm
Content-Type: application/json

{
  "paymentKey": "payment_key_from_toss",
  "orderId": "order_id",
  "amount": 15000
}
```

**결제 내역 조회**
```http
GET /api/v1/payments/my?page=0&size=10
Authorization: Bearer {accessToken}
```

**환불 요청**
```http
POST /api/v1/payments/{paymentId}/refund
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "reason": "PASSENGER_REQUEST|DRIVER_REQUEST|SYSTEM_ERROR",
  "description": "운행 취소로 인한 환불"
}
```

</details>

### **📊 공통 응답 형식**

#### **성공 응답**
```json
{
  "success": true,
  "data": {
    // 응답 데이터
  },
  "timestamp": "2024-01-20T10:30:00Z"
}
```

#### **에러 응답**
```json
{
  "success": false,
  "error": {
    "code": "ACC001",
    "message": "이미 사용 중인 이메일입니다",
    "timestamp": "2024-01-20T10:30:00Z"
  }
}
```

#### **에러 코드 체계**
| 서비스 | 코드 범위 | 예시 |
|--------|-----------|------|
| **Account** | ACC001~099 | ACC001: 중복 이메일, ACC004: 잘못된 인증 정보 |
| **Dispatch** | DIS001~099 | DIS001: 배차 요청 실패, DIS002: 기사 배정 실패 |
| **Trip** | TRP001~099 | TRP001: 운행 시작 실패, TRP002: 요금 계산 오류 |
| **Payment** | PAY001~099 | PAY001: 결제 실패, PAY002: 환불 실패 |

---

## 🏗 인프라 설계

### **🎯 마이크로서비스 아키텍처**

**(추후 인프라 아키텍처 이미지로 대체 예정)**

---

## 📏 개발 컨벤션

### **🎨 코드 스타일 가이드**

#### **Java 코딩 컨벤션**
- **언어**: Java 17 기준
- **빌드 도구**: Gradle 8.14
- **인덴테이션**: 4 spaces (탭 사용 금지)
- **라인 길이**: 최대 120자
- **인코딩**: UTF-8

#### **네이밍 컨벤션**
```java
// 클래스: PascalCase
public class UserRegistrationService

// 메소드/변수: camelCase  
public String getUserName()
private int userCount

// 상수: UPPER_SNAKE_CASE
public static final String DEFAULT_ROLE = "PASSENGER"

// 패키지: lowercase
com.gooddaytaxi.account.domain.model

// 테스트: TestCase로 끝나지 않고 Test로 끝남
public class UserRegistrationServiceTest
```

#### **파일 구조 컨벤션**
```
src/main/java/com/gooddaytaxi/{service}
├── application/
│   ├── usecase/           # 비즈니스 로직 유스케이스
│   ├── port/              # 인터페이스 정의 
│   └── dto/               # 애플리케이션 계층 DTO
├── domain/
│   ├── model/             # 엔티티 및 값 객체
│   ├── service/           # 도메인 서비스
│   ├── repository/        # 레포지토리 인터페이스
│   └── exception/         # 도메인 예외
├── infrastructure/
│   ├── persistence/       # 데이터베이스 구현
│   ├── external/          # 외부 API 호출
│   └── messaging/         # 메시지 큐 구현
└── presentation/
    ├── controller/        # REST 컨트롤러
    ├── dto/              # API 요청/응답 DTO
    └── config/           # Spring 설정
```

### **🗃 데이터베이스 컨벤션**

#### **테이블 명명 규칙**
```sql
-- 테이블명: snake_case, 복수형
CREATE TABLE users;
CREATE TABLE driver_profiles;
CREATE TABLE dispatch_assignment_logs;

-- 컬럼명: snake_case
user_id, created_at, phone_number

-- 인덱스명: idx_{table}_{columns}
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_dispatches_status_created ON dispatches(status, created_at);

-- 외래키 제약조건: fk_{table}_{ref_table}_{ref_column}
CONSTRAINT fk_driver_profiles_users_user_id
```

#### **UUID 사용 원칙**
```java
// 모든 Primary Key는 UUID 사용
@Id
@GeneratedValue(strategy = GenerationType.AUTO)
@Column(name = "user_id", updatable = false, nullable = false)
private UUID userId;

// 외래키도 UUID 타입으로 매핑
@JoinColumn(name = "user_id", referencedColumnName = "user_id")
private User user;
```

### **🔄 API 설계 컨벤션**

#### **REST API 명명 규칙**
```http
# 리소스명: 복수형 명사
GET /api/v1/users
GET /api/v1/dispatches

# 계층 구조 표현
GET /api/v1/users/{userId}/trips
GET /api/v1/dispatches/{dispatchId}/assignments

# 동사는 경로가 아닌 HTTP 메소드로 표현
POST /api/v1/dispatches (배차 생성)
POST /api/v1/dispatches/{dispatchId}/accept (배차 수락)
DELETE /api/v1/dispatches/{dispatchId} (배차 취소)
```

#### **응답 형식 통일**
```java
// 성공 응답 래퍼
@Getter
@AllArgsConstructor
public class ApiResponse<T> {
    private boolean success = true;
    private T data;
    private LocalDateTime timestamp = LocalDateTime.now();
}

// 에러 응답 래퍼  
@Getter
@AllArgsConstructor
public class ErrorResponse {
    private boolean success = false;
    private ErrorInfo error;
    private LocalDateTime timestamp = LocalDateTime.now();
}
```

### **📝 커밋 메시지 컨벤션**

#### **커밋 메시지 형식**
```
type: subject

body

footer
```

#### **타입 분류**
```bash
feat:     새로운 기능 추가
fix:      버그 수정  
docs:     문서 변경
style:    코드 포맷팅, 세미콜론 누락 등
refactor: 코드 리팩토링
test:     테스트 코드 추가/수정
chore:    빌드 업무, 패키지 매니저 설정 등
```

#### **커밋 메시지 예시**
```bash
# 기능 추가
feat: add master admin role separation

# 버그 수정  
fix: resolve passenger slack ID retrieval issue

# 테스트 추가
test: add unit tests for user registration service

# 문서 업데이트
docs: update API specifications and ERD diagram
```

### **🚀 브랜치 전략**

#### **Git Flow 적용**
```bash
# 브랜치 명명 규칙
main              # 운영 배포 브랜치
dev               # 개발 통합 브랜치  
feat/역할/#이슈번호  # 기능 개발 브랜치 (예: feat/account/#123)
```

---

## ⚡ 핵심기능

### **🎯 비즈니스 핵심 플로우**

#### **1. 사용자 관리 시스템**

**주요 기능**
- **다중 역할 지원**: 승객, 기사, 일반관리자, 최고관리자 4가지 역할
- **역할별 권한 제어**: RBAC 기반 세밀한 접근 제어
- **실시간 인증**: JWT 기반 무상태 인증 시스템
- **프로필 관리**: 사용자별 맞춤 정보 관리

#### **2. 스마트 배차 시스템**

**주요 특징**
- **지능형 매칭**: 거리 기반 최적 기사 매칭
- **실시간 처리**: 30초 내 응답 시간 보장
- **재시도 로직**: 최대 3회 자동 재배정 시도
- **상태 추적**: 실시간 배차 진행 상황 모니터링

#### **3. 운행 관리 & 요금 계산**

**요금 계산 로직**
```java
public class FareCalculationEngine {
    // 기본 요금 + (거리 요금 × 추가거리) + (시간 요금 × 운행시간)
    public BigDecimal calculateFare(Trip trip) {
        FarePolicy policy = getCurrentPolicy();
        
        BigDecimal baseFare = policy.getBaseFare();
        BigDecimal distanceFare = calculateDistanceFare(trip, policy);
        BigDecimal timeFare = calculateTimeFare(trip, policy);
        
        return baseFare.add(distanceFare).add(timeFare);
    }
}
```

#### **4. 안전한 결제 시스템**

**결제 특징**
- **다중 결제**: 카드/현금 결제 동시 지원
- **외부 연동**: Toss Payments 안전 결제
- **즉시 환불**: 자동화된 환불 처리 시스템
- **결제 이력**: 상세 결제 내역 관리

### **🔄 실시간 이벤트 처리**

#### **Event-Driven 아키텍처**
- **이벤트 발행**: UserRegistered, DispatchRequested, DispatchAccepted, TripStarted, TripEnded, PaymentCompleted
- **Kafka Topics**: user-events, dispatch-events, trip-events, payment-events
- **이벤트 구독**: 알림 서비스, 통계 서비스, 감사 로그, 외부 연동

### **🚀 고성능 최적화**

#### **캐싱 전략**
| 데이터 유형 | 캐시 위치 | TTL | 갱신 전략 |
|-------------|-----------|-----|-----------|
| **사용자 세션** | Redis | 30분 | Sliding Window |
| **기사 위치** | Redis | 5분 | 실시간 업데이트 |
| **요금 정책** | Redis | 1시간 | 정책 변경시 갱신 |
| **배차 락** | Redis | 30초 | 배차 완료시 삭제 |

#### **동시성 제어**
```java
@RedisLock(key = "dispatch:#{dispatchId}", timeout = 30000)
public void assignDriver(UUID dispatchId, UUID driverId) {
    // 동시에 여러 기사가 같은 배차를 수락하는 것을 방지
    Dispatch dispatch = dispatchRepository.findById(dispatchId);
    if (dispatch.getStatus() != PENDING) {
        throw new AlreadyAssignedException();
    }
    dispatch.assignDriver(driverId);
}
```

---

## 🔐 인증/인가 흐름도

![인증_인가 흐름도](https://github.com/user-attachments/assets/f642b5eb-d52b-42c4-9110-ed21e8cc1dff)

---

## 🔧 트러블슈팅

## 기사 회원가입 500 오류 - 전우선 -

### 원인
- `User` ↔ `DriverProfile` **JPA 양방향 연관관계**
- JSON 직렬화 시 **순환참조 발생**
- `StackOverflowError`로 인해 500 Internal Server Error 발생

### 해결
- 엔티티 직접 반환 제거
- **Response DTO 분리 적용**
- 순환참조 및 엔티티 노출 문제 해결

### 결과
- 기사 / 승객 회원가입 정상 동작
- API 응답 구조 안정화


---

## 🌐 공통 관심사항

### **🔄 횡단 관심사 (Cross-Cutting Concerns)**

#### **로깅 & 모니터링**
- **구조화된 로깅**: JSON 형태의 일관된 로그 포맷
- **분산 추적**: 요청 ID 기반 서비스 간 추적
- **메트릭 수집**: Prometheus + Grafana 실시간 모니터링
- **알림 시스템**: Slack 연동 장애 알림 자동화

#### **예외 처리**
```java
// 글로벌 예외 처리기
@RestControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(BusinessException.class)
    public ResponseEntity<ErrorResponse> handleBusinessException(BusinessException e) {
        log.error("Business error occurred: {}", e.getMessage(), e);
        return ResponseEntity
            .status(e.getErrorCode().getStatus())
            .body(ErrorResponse.of(e.getErrorCode()));
    }
    
    @ExceptionHandler(ValidationException.class)
    public ResponseEntity<ErrorResponse> handleValidationException(ValidationException e) {
        log.warn("Validation error: {}", e.getMessage());
        return ResponseEntity.badRequest()
            .body(ErrorResponse.of("VALIDATION_ERROR", e.getMessage()));
    }
}
```

#### **데이터 검증**
- **입력 검증**: Bean Validation (JSR-303) 활용
- **비즈니스 검증**: 도메인 계층에서 비즈니스 규칙 검증
- **데이터 무결성**: 데이터베이스 제약조건과 애플리케이션 검증 이중화

#### **트랜잭션 관리**
```java
@Transactional
public class DispatchService {
    
    // 읽기 전용 트랜잭션 최적화
    @Transactional(readOnly = true)
    public List<Dispatch> getMyDispatches(UUID userId) {
        return dispatchRepository.findByUserId(userId);
    }
    
    // 복잡한 비즈니스 로직의 트랜잭션 경계
    @Transactional
    public void processDispatchAcceptance(UUID dispatchId, UUID driverId) {
        // 배차 상태 변경, 기사 배정, 이벤트 발행까지 하나의 트랜잭션
    }
}
```

---

## 🤔 회고

## 잘한 점
- 마이크로서비스 아키텍처로 서비스 분리 성공
- Clean Architecture 적용으로 계층 간 의존성 관리
- JWT 기반 인증 및 역할별 권한 분리 구현
- Event-Driven 방식으로 서비스 간 느슨한 결합 달성
- Git Flow 전략 및 브랜치 명명 규칙 일관성 유지

## 어려웠던 점
- 배차 시스템 동시성 처리 (여러 기사 동시 수락 문제)
- 마이크로서비스 간 데이터 정합성 보장
- DB 스키마 변경 시 서비스 간 호환성 유지
- Kafka 이벤트 처리 순서 및 실패 처리 로직 설계
- 공통 모듈(`common-jpa`, `common-core`) 의존성 관리

## 한계점과 발전계획

### 한계점
- 테스트 코드 커버리지 부족
- 로깅 시스템 미완성
- 성능 최적화 부족 (캐싱, 쿼리 튜닝)

### 발전계획
- 단위 테스트 및 통합 테스트 추가
- Redis 캐싱 전략 구체화
- API 문서화 및 Swagger 활용도 개선

## 협업에서 아쉬운 부분
-
-
-
---

## 👥 팀원 소개

### **개발팀 소개**

| 역할     | 이름  | 담당 영역            | GitHub                            |
|--------|-----|------------------|-----------------------------------|
| **팀장** | 진주양 | DisPatch Service | [@juyangjin](https://github.com/juyangjin)   |
| **부팀장** | 이호준 | Trip Service     | [@jake8771](https://github.com/jake8771) |
| **팀원** | 고민정 | Support Service  | [@minjko](https://github.com/minjko) |
| **팀원** | 김진비 | Payment Service  | [@wlsql852](https://github.com/wlsql852) |
| **팀원** | 전우선 | Account Service  | [@wooxexn](https://github.com/wooxexn) |

---

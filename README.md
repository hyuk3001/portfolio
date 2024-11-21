# 🚀 지속적인 발전을 통해 혁신적인 시스템을 개발하는 개발자가 되겠습니다.
---

# :pushpin: **Intro**

## 💡 **SKILL & STACK**

### 🚀 **BackEnd**
- **Java 1.6**: 초기 프로젝트에서 Java 1.6 버전 사용하여 시스템 구현 경험  
- **Java 17**: 최신 Java 버전으로 **Spring Boot** 기반의 백엔드 시스템 설계 및 개발 경험  
- **Spring Boot**: RESTful API 및 모놀리식 아키텍쳐 구축, 빠른 개발과 유지보수성 향상
- **Spring Framework**: Spring의 다양한 모듈을 활용한 웹 애플리케이션 개발 및 관리
- **JPA (Java Persistence API)**: 객체와 관계형 데이터베이스 간 매핑 및 관리
- **MyBatis**: SQL 매핑 프레임워크로 SQL 쿼리 작성과 실행 처리, 성능 최적화 경험

### 📊 **Database**
- **MySQL**: 데이터베이스 설계 및 최적화, 쿼리 성능 개선

### ⚙️ **IDE**
- **VSCode**: 효율적인 프론트엔드 개발 및 디버깅
- **IntelliJ IDEA**: 백엔드 개발, Spring Boot 및 JPA 개발 환경 설정

---

# :pushpin: **Projects**
## 1. [실전 프로젝트 - K-pop 팬페이지](https://github.com/2024-AISCHOOL-WEB2B/Fanpage_back)
**BERT 기반 혐오 표현 필터링 기능을 제공하는 K-pop 팬페이지 서비스**  
**개발 기간**: 2024.10.15 ~ 2024.11.25

### 🎯 **프로젝트 목표**
- K-pop 팬들이 안전하고 즐겁게 소통할 수 있는 **K-pop 팬페이지** 서비스 구축
- **결제 시스템**을 통해 팬들이 굿즈를 구매하고 서비스를 이용할 수 있도록 구현

### 🔧 **개발 환경**
- **Java Version**: 17  
- **IDE**: IntelliJ IDEA  
- **Framework**: Spring Boot 3.2.10  

### 🌐 **기술 스택**
- **Server**: Apache  
- **Database**: MySQL  
- **WAS**: Tomcat  
- **ORM**: JPA  
- **Cloud**: AWS (S3, Parameter Store)

---

### 🛠️ **담당 역할 (Backend 개발)**

#### 🔑 **1. 백앤드 구조 설계**
- **폴더 구조 설계**:  
  - `config`, `controller`, `domain`, `DTO`, `exception`, `repository`, `service`, `util` 등으로 **모듈화된 폴더 구조** 설계  
  - 각 모듈을 담당하는 역할을 명확하게 구분하여 유지보수성을 강화
- **JPA 엔티티 설계**:  
  - 데이터베이스 스키마를 기반으로 **모든 JPA 엔티티 설계**  
  - `Builder` 패턴을 통해 **객체 생성**의 가독성을 높이고 **유지보수성** 강화
- **AWS Parameter Store 관리**:  
  - 민감한 정보를 안전하게 **AWS Parameter Store**에 저장하여 보안성을 강화

#### 💳 **2. 결제 서비스 개발**
- **주요 기능 구현**:  
  - **주소**, **카드**, **상품**, **포인트**에 대해 **조회**, **추가**, **수정**, **삭제**, **소모**, **복구** 기능을 구현하여 <br>결제 페이지에서 사용자가 필요한 모든 정보를 자유롭게 관리할 수 있도록 설계
- **결제 사전 정보 관리**:  
  - 사전 정보 등록, 검증, 주문 취소, 주문 번호 생성 기능을 통해 **안정적인 결제 환경 제공**
- **비동기 처리 최적화**:  
  - **비동기 방식**으로 결제 관련 정보를 처리하여 응답 속도를 최적화
  - **병렬 처리**를 통해 데이터베이스 조회 작업을 최적화하고, 사용자 경험을 개선
- **DTO 객체 생성 최적화**:  
  - **Builder 패턴**을 통해 DTO 객체를 직관적이고 **가독성 있게 생성**  
  - **메서드 체이닝**을 통해 결제 관련 데이터를 효율적으로 가공하여 코드 간소화 및 유지보수성 향상
- **보안성 강화**:  
  - 카드 정보 **암호화 및 복호화** 기능을 **AESUtil** 클래스를 사용하여 안전하게 처리

---

### 🛠️ **트러블 슈팅**

#### 1) **JPA 연관 문제 해결**
- **문제 발생**:  
  - 초기 설정에서 **JPA와 데이터베이스 연결 후**, 프로젝트 실행 시마다 데이터베이스 구조가 변경되는 현상 발생  
  - 테이블의 `Comments` 가 **제거되거나 `length` 속성**이 변경되는 문제 확인
- **원인 분석**:  
  - `@Entity`로 엔티티를 설정할 때 **JPA에서 자동으로 테이블 구조를 조정**하는 기능이 활성화되어, 스키마 업데이트 시 테이블 구조가 변경되는 현상 발생
- **해결 방법**:  
  1. `spring.jpa.hibernate.ddl-auto` 설정을 **`update`**에서 **`validate`**로 변경하여 자동 수정을 방지
  2. 엔티티를 수정할 경우, **테이블 구조에 변경이 필요한지 여부를 논의**한 후 일시적으로 `ddl-auto`를 **`update`**로 변경하여 수정

#### 2) **AWS S3와 AWS Parameter Store 통합 이슈 해결**
- **초기 S3 연결 방식**:  
  - AWS SDK 1.x를 사용하여 **S3와 Spring Boot를 독립적으로 연결**
- **문제 발생**:  
  - **AWS Parameter Store**를 도입하면서 **민감한 정보를 안전하게 저장**하려고 했으나 **Spring Cloud AWS와의 호환성 문제**로 Parameter Store에 접근하지 못하는 현상 발생
    ![image (2)](https://github.com/user-attachments/assets/4b3382c8-6c4b-4359-a46f-3c3420ccced1)
- **원인 분석**:  
  - Spring Boot 3.2.x는 **Spring Cloud AWS 3.1.x 이상**과 호환되며, 이 조합에서 **AWS SDK 2.x** 사용이 필수였음.  
  - 기존 S3 연결 방식이 **AWS SDK 1.x**를 사용하고 있었기 때문에 **충돌 발생**
    ![image](https://github.com/user-attachments/assets/c08ed607-21a1-4b3e-a762-f4b5cfda7ce6)
- **해결 방법**:  
  1. 기존 S3 클라이언트를 **SDK 2.x의 S3Client**로 마이그레이션
  2. **AWS CLI 설치 및 IAM 액세스 설정**하여 인증 및 권한 부여

[프로젝트 바로가기](https://github.com/2024-AISCHOOL-WEB2B/Fanpage_back)<br>

---

## 2. [실전 프로젝트 - 의류 추천 서비스](https://github.com/2024-AISCHOOL-WEB2B/coorde.git)
**통계적 기법을 이용한 몸에 맞는 의류 추천 서비스**  
**개발 기간**: 2024.07.02 ~ 2024.08.02

### 🔧 **사용 기술**
- **Java**, **JS**, **Spring MVC**, **Mybatis**  
- **MySQL**, **Python**, **Apache Tomcat**

---

### 🛠️ **담당 역할 (Backend 개발)**
#### 페이지 메인기능 구현
- 의류페이지 정렬, 필터링 기능 구현  
- 사용자 및 관리자 페이지의 **문의사항 확인** 구현  
- **장바구니 페이지** 별점 기능 구현  

#### 주요 페이지
![메인페이지](/mainpage.png)  
![마이페이지](/mypage.png)

---

### 🛠️ **트러블 슈팅**  
- **문제 발생**  
  - JSP 파일에서 자바스크립트 리터럴(``)을 사용하여 변수 값을 삽입하려고 할 때 에러 발생  
- **원인 분석**  
  - `${}` 구문이 JSP의 EL식으로 해석되어 오류 발생  
- **해결 방법**  
  - JSP에서 자바스크립트 리터럴을 사용할 때 `${}` 앞에 **역슬래시(\)**를 추가하여 JSP가 이를 자바스크립트 구문으로 인식하도록 적용  
  - 이를 통해 정상적인 변수 삽입 처리

![에러](/error.png)

[프로젝트 바로가기](https://github.com/2024-AISCHOOL-WEB2B/coorde.git)

---

# :pushpin: **Education**
> * 2023.09.27 ~ 2024.04.17  
> 스마트인재개발원 1040시간(6개월) **언어지능기반 분석서비스모델 개발자과정** 수료  

---

# :pushpin: **Contact**
- 📧 이메일: cksgur2297@naver.com  
- 👨‍💻 깃허브: [https://github.com/hyuk3001](https://github.com/hyuk3001)

---

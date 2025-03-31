# ddd-starter

## DDD 적용 이전 기존 개발의 문제점

### 빈약한 도메인 모델 (Anemic Domain Model) & 서비스 계층 비대화

> 도메인 객체 (Entity) 가 행위(기능)이 없이 단순히 데이터 필드와 Getter/Setter 만 가진 데이터 덩어리로 전락
> 이로 인하여 OOP 의 장점인 캡슐화를 사용할 수 없어지며, 비즈니스 로직이 이곳저곳에 흝어져 코드의 응집도가 매우 낮아짐.

### 유비쿼터스 랭귀지 (Ubiquitous Language) 부재 & 소통의 벽

> 도메인 전문가와 개발자 사이의 통일된 용어가 없어서 같은 용어를 다른 뜻으로 이해하는 오해가 발생함.

### 암묵적인 도메인 개념 & 숨겨진 비즈니스 규칙

> 비즈니스 규칙이 서비스 레벨 및 심지어 데이터베이스 쿼리로 나누어져 있어 비즈니스 규칙의 전반을 파악하기 어려우며 수정도 어려움.

### 낮은 응집도 & 높은 결합도

> 비즈니스 로직이 이곳저곳에 흝어져 있어 코드의 응집도가 매우 낮아지며, 서비스 레벨에서 기술적인 코드들과 비즈니스가 혼재되면서
> 저수준의 코드(기술적인 코드) 및 관련성이 부족한 코드들과의 결합도가 높아짐.

### 기술 중심 설계 & 도메인 지식 경시

> 데이터베이스 및 외부 연동 기술 중심으로 설계하여 도메인 자체보다는 기술에 도메인을 끼워넣게됨. 이로인해서 코드가 부자연스러워져
> 테스트 및 비즈니스의 변화에 유연하게 대응이 힘들어짐.

---

## 전술적 설계(Tactical Design)

> "개별 Bounded Context 내부" 에서 "도메인 모델" 을 구체적인 "객체 (Object)" 와 "클래스 (Class)" 로 어떻게 구현할 것인가에 대한 "세부적인 설계 기법" 들을 다루는 영역
> 핵심 목표:
> * 풍부하고 표현력 있는 도메인 모델 구축: 도메인 전문가의 언어 (유비쿼터스 랭귀지) 를 코드로 정확하게 표현하고, 도메인의 복잡성을 잘 담아내는 모델을 만드는 것.
> * 견고하고 유지보수하기 쉬운 코드 작성: 객체지향 원칙 (캡슐화, 단일 책임 원칙 등) 을 잘 지키고, 응집도는 높고 결합도는 낮은 코드를 만드는 것.
> * 테스트 용이성 확보: 도메인 로직을 외부 의존성 없이 쉽게 테스트할 수 있도록 설계하는 것.

### 핵심 개념

> * 값 객체 (Value Object - VO)
> * 엔티티 (Entity)
> * 애그리거트 (Aggregate) & 애그리거트 루트 (Aggregate Root)
> * 리포지토리 (Repository)
> * 도메인 서비스 (Domain Service)
> * 도메인 이벤트 (Domain Event)
> * 팩토리 (Factory)

---

## 전략적 설계(Strategic Design)

> "복잡한 도메인" 을 "관리 가능한 단위" 로 나누고, "각 단위 간의 관계" 를 정의하며, "팀 구조" 와 "개발 전략" 을 수립하는
> "거시적인 설계 활동". "코드 레벨" 의 구체적인 설계 (전술적 설계) 에 들어가기 전에, "시스템 전체의 청사진" 을 그리는 과정
>
> 전략적 설계는 "한 번" 하고 끝나는 것이 아니라, "지속적인 과정" 이야! 시스템이 진화하고 비즈니스가 변화함에 따라, Bounded Context 경계는 재조정될 수 있고, 컨텍스트 맵은 업데이트되어야 해.
> 끊임없이 도메인을 탐구하고, 모델을 개선해 나가는 "반복적인 노력" 이 필요하지!

### 핵심 개념

> * 도메인 (Domain) & 하위 도메인 (Subdomain): 문제 영역 분석
> * Bounded Context (바운디드 컨텍스트): 모델 경계 설정
> * 유비쿼터스 랭귀지 (Ubiquitous Language): 공통 언어 구축
> * 컨텍스트 맵 (Context Map): 관계 정의 및 시각화
> * 다양한 관계 패턴 (Partnership, Shared Kernel, Customer-Supplier, Conformist, ACL, OHS, Published Language, Separate Ways)

---

## 심화 개념

> * 도메인 이벤트 (Domain Event)
> * 모듈 (Module)
> * 애플리케이션 서비스(Application Service)

---

## 구현 아키텍처

> 핵심 원칙: 이 아키텍처들은 모두 "도메인 모델을 시스템의 핵심에 두고 보호" 하고, "관심사를 명확하게 분리" 하며, "의존성 역전 원칙 (DIP)" 을 활용하여 "계층 간 결합도를 낮추는 것" 을 목표로 해!

### 종류

> * 계층형 아키텍처(Layered Architecture)
> * 헥사고날 아키텍처(Hexagonal Architecture)
> * 클린 아키텍처(Clean Architecture)
> * 양파 아키텍처(Onion Architecture)

### CQRS(Command Query Responsibility Segregation) 패턴

> CQRS 는 말 그대로 "명령 (Command)" 과 "조회 (Query)" 의 "책임 (Responsibility)" 을 "분리 (Segregation)" 하는 아키텍처 패턴이야.
> * Command (명령): 시스템의 상태를 변경하는 모든 작업 (예: 생성, 수정, 삭제). "Write" 작업에 해당.
> * Query (조회): 시스템의 상태를 읽는 모든 작업. "Read" 작업에 해당. 상태를 변경하지 않음!
>
> 핵심 아이디어: "상태를 변경하는 책임" 과 "상태를 조회하는 책임" 을 완전히 다른 모델과 경로로 처리하자는 거야. 하나의 모델로 두 가지 책임을 모두 감당하려고 하면 모델이 복잡해지고, 각 책임에 최적화하기
> 어렵다는 문제의식에서 출발했어.
>
> Eventual Consistency    
> 핵심 개념: 시스템에 새로운 변경 사항 (Update) 이 더 이상 발생하지 않는다면, 일정 시간이 지난 후에는 모든 복제본 (Replica) 이 결국 (Eventually) 동일한 값으로 수렴 (
> Converge) 하는 것을 보장한다.

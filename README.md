# ddd-starter

## DDD 적용 이전 기존 개발의 문제점
### 빈약한 도메인 모델 (Anemic Domain Model) & 서비스 계층 비대화
> 도메인 객체 (Entity) 가 단순히 데이터 필드와 Getter/Setter 만 가진 "데이터 덩어리" (Data Class) 로 전락

### 유비쿼터스 랭귀지 (Ubiquitous Language) 부재 & 소통의 벽
> 도메인 전문가 (기획자, 현업 담당자 등) 와 개발자가 사용하는 "용어" 가 서로 달라. 같은 개념을 두고도 서로 다른 단어를 사용하거나, 
> 같은 단어를 다른 의미로 해석하는 경우가 비일비재

### 암묵적인 도메인 개념 & 숨겨진 비즈니스 규칙 
> 예를 들어, "특별 할인 정책" 이나 "환불 규정" 같은 복잡한 규칙들이 코드 여기저기에 숨겨져 있어서, 전체 그림을 파악하기 어렵고, 
> 규칙을 수정하거나 새로운 규칙을 추가하기가 매우 까다로워.

### 낮은 응집도 & 높은 결합도
> 명확한 "경계 (Boundary)" (예: Bounded Context, Module) 없이 개발하다 보면, 서로 다른 도메인 개념들이 마구 뒤섞이고, 
> 코드들이 거미줄처럼 얽히게 돼. 하나의 기능을 수정하면 예상치 못한 다른 기능에서 오류가 발생하는 "사이드 이펙트 (Side Effect)" 가 
> 빈번하게 일어나지.

### 기술 중심 설계 & 도메인 지식 경시
> 소프트웨어 설계를 할 때 "핵심 도메인" 의 요구사항과 비즈니스 규칙보다는 "사용할 기술" (데이터베이스 스키마, 프레임워크, 라이브러리 등) 에 
> 더 집중하는 경향이 있어. 데이터베이스 테이블 구조를 먼저 설계하고, 그 구조에 맞춰서 도메인 객체를 "끼워 맞추는" 방식으로 개발하는 경우가 많지.

---

## 전략적 설계()
> 

### Event Storming
> 

### 도메인
>

### 유비쿼터스 언어
>

### Bounded Context
>

### Context Map
>

---

## 전술적 설계
>

### 애그리거트 루트
>

### 엔티티(Entity)
> 

### 값 객체(Value Object)
>

### 애그리거트(Aggregate)
>

### 애그리거트 루트(Aggregate root)
>

### 리포지토리(Repository)
>

### 모듈(Module)
> 

### 도메인 서비스
> 

### 팩토리
>

### 도메인 이벤트
> 

---

## 구현 아키텍처
### Layered 아키텍처
>

### Clean 아키텍처
> 

### Hexagonal 아키텍처
>

---

## CQRS(Command Query Responsibility Segregation) 패턴
> 
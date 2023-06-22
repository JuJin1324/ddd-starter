# ddd-starter

## 개념
### Bounded Context
>

### Context Map
>

### 애그리거트(Aggregate)
>

### 명령(Command)
>

### 이벤트(Event)
> 

---

## 설계
### Event Storming
> 명령(Command), 애그리거트(Aggregate), 이벤트(Event) 에 대한 전체적 설계  
> 1.명령(Command) 와 그에 따라 발생하는 이벤트(Event)들의 흐름을 나열한다.  
> 2.관련있는 명령과 이벤트들을 한데 묶어 정리한다.   
> 3.묶어놓은 명령과 이벤트들을 기반으로 애그리거트를 지정한다.  
> 4.묶어놓은 명령, 이벤트 그리고 애그리거트를 바운디드 컨텍스트로 묶는다.  
> 5.개발을 진행하면서 변경되어야 하는 명령, 이벤트 또는 애그리거트가 있으면 변경한다.  


---

## 구현 아키텍처
### Layered 아키텍처
> 
> 
> 도메인 패키지의 경우 rootPackage 아래 `domain` 패키지를 만들지 않고 `<rootPackage>.<domain 명>` 로 만든다.    
> 예를 들어 rootPackage 가 `starter.ddd` 이고 주문 도메인을 만든다고 하면 `starter.ddd.order` 로 주문 도메인 패키지를
> 만들 수 있다.
>
> 도메인 패키지 안의 구조는 다음과 같다.  
> `application`: 표현 영역(Controller) 에서 사용할 응용 서비스(@Service) 들이 위치한다.
>
> `domain`: 비즈니스 로직을 담은 도메인이 위치하는 영역으로 엔티티(Entity), 저장소(Repository), 도메인 서비스가 위치한다.  
> domain 패키지 안에 클래스가 많아지면 다음과 같이 분리한다.  
> domain.model: 엔티티 및 밸류 타입을 위치한다.  
> domain.repository: 저장소가 위치한다.  
> domain.service: 도메인 서비스가 위치한다.
>
> `infra`: 도메인 서비스 구현 코드가 위치한다.
 

### Clean 아키텍처
> 

### Hexagonal 아키텍처
> 

---

## 테스트
### 단위테스트
> 

### 통합테스트
> 

# ddd-starter

## 개념
### 도메인
> 먼저, 도메인이라는 것은 '영역'을 말한다. 그러니 비즈니스상에서 도메인이란 '업무의 집합'이라고 봐야한다.
> 예를 들어서 스타벅스는 '커피' 도메인이고, 버거킹은 '음식' 도메인이다.
> 서브 도메인이라고 해서 더 구체적으로 쪼갤 수도 있지만, 가장 큰 틀에서 도메인의 의미는 위와 같다고 보면 된다.  
> 
> 도메인을 쉽게 이해하기 위해 음식 주문 배달 애플리케이션을 만든다고 가정한다.  
> 음식 주문 배달 애플리케이션은 음식을 주문하는 고객, 주문받은 음식을 만들고 판매하는 음식점, 
> 완성된 음식을 배달하는 배달원, 해당 음식을 주문하고 결제하는데 이용되는 카드사 또는 은행이 필요하다.  
> 이들을 각각의 도메인이라 부를 수 있다.  
> 이렇게 애플리케이션을 구현하기 위해 필요한 업무들을 자세히 구분하면 좋은 애플리케이션을 만들 가능성이 높아진다.  
> 해당 업무에서 고객이 음식을 주문하는 과정, 주문받은 음식을 처리하는 과정, 조리된 음식을 배달하는 과정 등 
> 도메인 지식(Domain Knowledge)들을 서비스 계층에서 비즈니스 로직으로 구현해야 하는 것이다.  
> 즉, 도메인은 현실에서 접하는 업무의 한 영역들을 말한다.  
> 
> 사용자가 사용하는 것을 도메인(Domain)이라고 합니다.  
> DDD는 소프트웨어를 이해하고 프로젝트를 성공적으로 완성하기 위한 사고방식이라고 할 수 있습니다.  
> 도메인은 사용자에 따라 또는 사용자가 바라보는 관점에 따라 지속적으로 변화합니다.  

### 기존 개발의 문제점
> 데이터베이스 위주의 개발 (데이터베이스 모델링을 중요시)     
> 서비스에는 흐름제어 로직밖에 없고 비즈니스 규칙과 개념들은 SQL에 존재한다. 이렇게 비즈니스 로직과 저장 기술이 강하게 결합되어 있는 
> 구조인 경우, 저장소를 변경하기 쉽지 않다. 또한 성능 측면에서 성능을 데이터베이스에 의존하게 된다. 
> 이러면 데이터가 많아졌을 때 데이터베이스의 성능은 지속적으로 떨어지고 이를 최적화 하기 위해 데이터베이스 서버의 사양과 용량을 
> 계속 증가시키고 쿼리 튜닝에 몰두할 수 밖에 없다. 클라우드 인프라를 사용한 자동 스케일 아웃은 의미가 없어진다. 
> 정작 바쁜 것은 데이터베이스이기 때문에 어플리케이션을 아무리 스케일 아웃해봐야 효과는 미미하다.
> 
> 트랜잭션 스크립트 패턴   
> 서비스(Spring에서 사용되는 Service를 말함)에 모든 비즈니스 로직이 있고 비즈니스 절차에 따라 도메인 객체를 이용해 처리한다. 
> 도메인 객체는 단지 속성값만 이용되는 정보 묶음의 역할만 하게 된다. 서비스는 유스케이스 처리의 단위이고 대부분의 비즈니스 로직 처리가 
> 서비스에서 이뤄지므로 비슷한 유스케이스의 경우 서비스에 중복되는 코드가 계속 생겨날 수 있고 이런한 점이 유지보수를 어렵게 한다. 
> 비즈니스 로직을 테스트하기 위해 Mocking을 해야하고 이는 테스트의 복잡성을 높이고 관리하기 어려운 테스트 코드를 발생시킨다.  
> 
> 도메인 모델 패턴  
> 도메인 객체가 속성뿐만 아니라 비즈니스 행위를 가지고 있어 책임을 수행하게 된다.
> 서비스의 책임들이 도메인으로 분산되기 때문에 서비스의 메서드는 단순해진다.
> 거대한 서비스 클래스 대신 각기 적절한 책임을 가진 여러 클래스로 구성되므로 이해하기 쉽고 관리 및 테스트하기 쉽다.
> 잘 정의된 도메인 모델은 코드양을 줄이고 재사용성도 높다.
> 도메인 모델 패턴은 도메인 주도 설계의 애그리거트 패턴을 적용할 수 있는 구조이다.

### 유비쿼터스 언어
> 프로젝트를 진행하다보면 다음과 같은 상황을 겪어볼 수 있다.  
> 첫번째 - 회원 관련  
> 사용자A : 신규 회원을 등록하겠습니다.  
> 사용자B : 신규 회원을 추가하겠습니다.  
> 사용자가 말하는 등록과 추가는 무슨 의미일까? 모두 신규 회원이 가입되었다는 의미로 사용하는 걸까?
> 
> 두번째 - 상품 관련  
> MD1 : 노트북 상품을 추가하겠습니다.  
> MD2 : 노트북 제품을 등록하겠습니다.  
> 사용자가 말하는 상품과 제품은 같은 의미로 사용하는 걸까? 
> 추가와 등록은 이전 회원에 비해 헷갈린다. 단순히 수량을 추가하는 걸까? 새롭게 상품&제품을 등록한다는 걸까?
> 
> 이렇듯 같은 팀내에서 도메인에 대한 용어가 제각각인 경우를 겪어본 적이 있을 거다. (혹은 용어가 같지만 다른 의미로 사용된 경우)
> 이런 차이로 같은 도메인을 서로 다르게 바라보고 각자 이해하게 되며, 나중에는 문제로 발전하는 상황이 올 수 있다. (개발자와 비개발자의 차이는 더욱 끔찍하다)
> 이를 해결하려면 어떻게 해야할까? 그에 관련해서 유비쿼터스 언어를 언급하려고 한다.
> 
> 특정 도메인에서 특정 용어가 해당 도메인에서의 의도를 명확히 반영하고, 도메인의 핵심 개념을 잘 전달할 수 있는 언어.  
> 모든 팀원이 특정 용어를 들었을 때 같은 것을 생각할 수 있는 명확하게 정의된 언어. 
> 같은 용어에 각자 다른 생각을 하거나 같은 것을 말하지만 용어가 다른 경우가 있으면 안된다.
> 도메인에서 사용하는 언어는 코드에 그대로 똑같이 반영되야 한다. 똑같이 반영되지 않으면 개발자는 해당 용어를 해석하고 이해해야하는 부담이 생긴다.
> 유비쿼터스 언어를 사용함으로써 코드의 가독성을 높여 코드를 분석하고 이해하는데 시간을 절약할 수 있다.
> 용어가 정의 될 때마다 용어 사전에 이를 기록하고 명확하게 정의 함으로써 추후 또는 다른 사람들도 공통된 언어를 사용할 수 있도록 한다.
> 
> 용어 사전 관리
> 모두가 이해하는 유비쿼터스 언어는 단순히 명사뿐만 아니라 동사까지 용어 사전으로 관리해야한다.
> 관리 방법은 JIRA, 파일 문서 등 다양하며, 편안한 방식으로 관리하면 된다.  
> ex) 상품  
> | 한글명 | 영문명 | 설명 | 
> | --- | --- | --- |
> | 상품 | Product | 식당에서 판매하는 음식, 음료를 지칭 |
> | 등록 | Register | 새로운 상품을 등록한다. | 
> | 가격 변경 | Change Price | 상품의 가격을 변경한다. 0원 이상 입력받아야 한다. |

### Bounded Context
> 도메인 영역의 경계  
> 바운디드 컨텍스트안에서는 유비쿼터스 언어를 사용해야한다.  
> 도메인 영역의 경계의 기준은 유비쿼터스 언어를 사용했을 때, 해당 용어의 개념이 달리지는 그 곳을 기준으로 경계를 나눈다. ex) 결제 컨텍스트, 배송 컨텍스트  
> 
> 고객이라는 도메인은 결제 도메인 입장에서는 신용카드 정보나 계좌 정보를 가진 **"결제자"**로서 사용되고 배송 도메인 입장에서는 상품을 받을 주소와 우편번호, 
> 전화번호를 소유한 **"수취자"**를 의미한다.  
> 도메인 모델은 특정한 컨텍스트 안에서 완전한 의미를 갖는다.  
> 바운디드 컨텍스트는 여러개의 서브 도메인으로 구성되고 하나의 서브 도메인은 한 바운디드 컨텍스트에 포함된다.  

### Context Map
> 컨텍스트 경계를 식별해 내고 이들간의 관계를 표현한 그림을 컨텍스트 맵(Context Map)이라 한다.  
> 컨텍스트간의 관계는 선으로 표현되고 U는 Upstream으로서 공급자, D는 Downstream으로서 수요자를 나타낸다. 즉 데이터가 흐르는 방향.  

### 참조사이트
> [도메인 주도 설계란? DDD란?](https://yoonbing9.tistory.com/121)  
> [유비쿼터스 언어(UBIQUITOUS LANGUAGE)](https://loopstudy.tistory.com/334)  

---

## 도메인 모델링
### 엔티티(Entity)
> 엔티티는 다른 엔티티와 구별할 수 있는 식별자를 가진 도메인의 실체 개념을 표현하는 객체이다.  
> 식별자는 고유하되 엔티티의 속성 및 상태는 계속 변할 수 있다.  
> 식별자가 있기 때문에 데이터베이스로 추적가능하다  

### 값 객체(Value Object)
> 값객체는 각 속성이 개별적으로 변화하지 않는 개념적 완전성을 모델링한다.  
> <도메인 주도 설계 핵심>의 저자 반 버논은 값객체의 특성을 다음과 같이 정의한다.  
> * 도메인 내의 어떤 대상을 측정하고, 수량화하고, 설명한다.  
> * 관련 특징을 모은 필수 단위로 개념적 전체를 모델링한다.  
> * 측정이나 설명이 변경될 땐 완벽히 대체 가능하다.  
> * 다른 값과 등가성을 사용해 비교할 수 있다.  
> * 값 객체는 일단 생성되면 변경할 수 없다.
> 
> 그 밖에 특성  
> * 밸류 타입은 불변
> * 시스템이 성숙함에 따라 데이터 값을 객체로 대체
> * 밸류 객체의 값을 변경하는 방법은 새로운 밸류 객체를 할당하는 것뿐이다.
> * 정말 String으로 우편 번호를 표현할 수 있는가?
> * 항상 equals() 메서드를 오버라이드할 것을 권고한다.
> * equals를 재정의하려거든 hashCode도 재정의하라 - Effective Java
> * VALUE OBJECT는 DTO가 아니다. - Martin Fowler

### 애그리거트(Aggregate)
> * 관련 객체를 하나로 묶은 군집(1~2개의 엔티티와, 값 객체, 표준타입(자바에서 enum)으로 구성)  
> * 애그리거트는 군집에 속한 객체들을 관리하는 루트 엔티티를 갖는다.
> * 이들 간에는 비즈니스 의존관계를 맺고 있으며 비즈니스 정합성을 맞출 필요가 있다. 따라서 애그리거트 단위가 트랜잭션의 기본 단위가 된다.
> * 애그리거트로 묶어서 바라보면 좀 더 상위 수준에서 도메인 모델 간의 관계를 파악할 수 있다.
> * 애그리거트는 응집력을 유지하고 애그리거트 간에는 느슨한 결합을 유지한다.
> * 애그리거트에 속한 객체는 유사하거나 동일한 라이프사이클을 갖는다.
> * 한 애그리거트에 속한 객체는 다른 애그리거트에 속하지 않는다.
> * 두 개 이상의 엔티티로 구성되는 애그리거트는 드물게 존재한다.(대부분 애그리거트 루트만 엔티티이다. 그 밖의 엔티티가 존재하면, 정말 그 객체가 엔티티가 맞는지 의심해봐야한다. 
> 혹은 드물게 운영상 데이터 추적 혹은 성능상의 이유로 엔티티로 만들기도 한다.)

### 애그리거트 루트(Aggregate root)
> * 애그리거트 내에 있는 엔티티 중 가장 상위의 엔티티를 애그리거트 루트로 정함.
> * 애그리거트 루트를 통해서만 애그리거트 내의 엔티티나 값 객체를 변경할 수 있다.(퍼사드 패턴과 유사)
> * 애그리거트간의 참조는 직접참조하지 않고 ID 참조를 한다.(그림에서 Order가 Buyer를 직접 참조하지 않고 BuyerID 로 참조하고 있다.)
> * 애그리거트는 단일 트랜잭션으로 일관성을 유지하지만 애그리거트간의 일관성이 필요하다면 도메인 이벤트를 통해 다른 애그리거트를 갱신해서 일관성을 유지한다.

### 리포지토리(Repository)
> * 엔티티나 밸류가 요구사항에서 도출되는 도메인 모델이라면 리포지터리는 구현을 위한 도메인 모델
> * 애그리거트 단위로 도메인 객체를 저장하고 조회하는 기능을 정의한다.
> * 애그리거트를 구하는 리포지터리 메서드는 완전한 애그리거트를 제공해야 한다.
> * 리포지터리가 완전한 애그리거트를 제공하지 않으면, 필드나 값이 올바르지 않아 애그리거트의 기능을 실행하는 도중에 NullPointerException 과 같은 문제가 발생하게 된다.
> * 리포지토리는 애그리거트(루트) 단위로 존재하며 테이블 단위로 존재하는 것이 아니다.(애그리거트 1 개 당 리포지토리 1 개)

### 도메인 서비스
> 여러 애그리거트가 필요한 기능 ex) 결제 금액 계산 로직  
> 
> * 상품 애그리거트: 구매하는 상품의 가격이 필요하다. 또한 상품에 따라 배송비가 추가되기도 한다.
> * 주문 애그리거트: 상품별로 구매 개수가 필요하다.
> * 할인 쿠폰 애그리거트: 쿠폰별로 지정한 할인 금액이나 비율에 따라 주문 총 금액을 할인한다. 
> 할인 쿠폰을 조건에 따라 중복 사용할 수 있다거나 지정한 카테고리의 상품에만 적용할 수 있다는 제약 조건이 있다면 할인 계산이 복잡해진다.  
> * 회원 애그리거트: 회원 등급에 따라 추가 할인이 가능하다.
> 이 상황에서 실제 결제 금액을 계산해야 하는 주체는 어떤 애그리거트일까?
> 
> 한 애그리거트에 넣기 애매한 도메인 개념을 구현하려면 애그리거트에 억지로 넣기보다는 도메인 서비스를 이용해서 도메인 개념을 명시적으로 드러내면 된다.
> 응용 영역의 서비스가 용용 로직을 다룬다면 도메인 서비스는 도메인 로직을 다룬다.
> 도메인 영역의 애그리거트나 밸류와 같은 다른 구성요소와 비교할 때 다른 점은 상태 없이 로직만 구현한다.
> 서비스를 사용하는 주체는 애그리거트가 될 수도 있고 응용 서비스가 될 수도 있다.
> 특정 기능이 응용 서비스인지 도메인 서비스인지 감을 잡기 어려울 때는 해당 로직이 애그리거트의 상태를 변경하거나 애그리거트의 상태 값을 계산하는지 검사해 보면 된다.
> 응용 서비스와 구분을 위해 통상 응용 서비스에는 @Service 어노테이션을, 도메인 서비스에는 @Component를 사용하기도 한다.

### 팩토리
> * 복잡한 객체를 생성해야한다면 생성 역할만 책임지는 Factory 에게 그 역할을 위임할 수 있다.  
> * 도메인 객체를 생성하기 위한 기존의 클라이언트 코드가 깔끔해진다.  
> 
> 팩토리의 생성 위치  
> * 애그리거트 루트의 정적 팩토리 메서드 - 애그리거트를 생성하기 좋은 위치
> * 도메인 서비스 - 다른 애그리거트를 이용하여 생성해야한다면 고려해보자
> * 별개의 팩토리 클래스 - 구상 구현체나 생성과정의 복잡성등을 감춰야 하는 경우(?)
> Factory는 자신의 생성물과 가장 밀접한 관계에 있는 위치에 있어야 한다. (만들어내는 객체와 매우 강하게 결합돼 있으므로)

### 도메인 이벤트
> 서비스간 정합성을 일치시키기 위해 단위 애그리거트의 주요 상태 값을 담아 전달되도록 모델링한다.  
> 이벤트의 용도는 후처리, 데이터 동기화 등  
> 도메인 이벤트를 사용하면 애그리거트간, 바운디드 컨텍스트간, 외부 서비스와의 결합을 느슨하게 한다.(도메인 로직이 섞이는 것을 방지)  
> 도메인 모델에서 이벤트 주체는 엔티티, 밸류, 도메인 서비스와 같은 도메인 객체이다.  
> 도메인 객체는 도메인 로직을 실행해서 상태가 바뀌면 관련 이벤트를 발생한다.  
> 스프링에서 제공하는 AbstractAggregateRoot 를 애그리거트 루트에 확장하면 애그리거트 루트 내에서 직접 이벤트를 발생할 수 있다
> (기존의 ApplicationEventPublisher을 사용하면 어플리케이션 레이어에서 이벤트를 발행해야한다)  
> 이벤트 핸들러는 서비스 레이어에서 구현하면 된다.  

---

## 설계
### 도메인 주도 설계
> 도메인 주도 설계는 크게 전략적 설계와 전술적 설계로 나뉩니다.  
> * 전략적 설계 - 도메인 전문가 및 기술팀이 함께 모여 유비쿼터스 언어를 통해 도메인 지식을 공유 및 이해하고 
> 이를 기준으로 개념과 경계를 식별해 바운디드 컨텍스트(bounded context)로 정의하고 경계의 관계를 컨텍스트 맵(context map)으로 정의하는 활동
> * 전술적 설계 - 전략적 설계에서 도출된 바운디드 컨텍스트와 도메인을 이용하여 애그리거트 패턴, 엔티티와 값 객체, 레포지토리 
> 등을 구성하고 구현하는 활동

### Event Storming
> 명령(Command), 애그리거트(Aggregate), 이벤트(Event) 에 대한 전체적 설계  
> 1.명령(Command) 와 그에 따라 발생하는 이벤트(Event)들의 흐름을 나열한다.  
> 2.관련있는 명령과 이벤트들을 한데 묶어 정리한다.   
> 3.묶어놓은 명령과 이벤트들을 기반으로 애그리거트를 지정한다.  
> 4.묶어놓은 명령, 이벤트 그리고 애그리거트를 바운디드 컨텍스트로 묶는다.  
> 5.개발을 진행하면서 변경되어야 하는 명령, 이벤트 또는 애그리거트가 있으면 변경한다.  
> 
> 다음과 같이 진행한다.  
> 도메인이벤트 식별 (30분) -> 커맨드 식별 (30분) -> 외부 시스템 도출 (20분)   
> -> 엑터 식별 (30분) -> 흐름 설명 (30분) -> 어그리게잇 식별(30분)   
> -> 컨텍스트 경계 정의(30분) -> 정책 식별(30분) -> 컨텍스트 매핑 (30분)  

### 참조사이트
> [마이크로서비스 모델링 ④ : 이벤트 스토밍을 통한 마이크로서비스 도출](https://engineering-skcc.github.io/microservice%20modeling/Event-Storming/)

---

## 구현 아키텍처
### Layered 아키텍처
> **Layered 아키텍처란?**  
> Layered Architecture는 말 그대로 계층이 나뉘어져 있는 아키텍쳐를 뜻한다.  
> Layered Architecture의 주된 목표는 각각의 layer는 하나의 관심사에만 집중할 수 있도록 하는 것이다.  
> 사용자 인터페이스(ui) -> 응용(application) -> 도메인(domain) -> 인프라스트럭처(infrastructure) 로 구성됨.  
> 상위 레이어에서 하위 레이어의 의존은 허용하고 있으나, 반대로 하위 레이어에서 상위 레이어로의 의존은 허용하고 있지 않습니다.  
> 좀 더 엄격하게 아키텍처를 적용한다면, 상위 레이어는 바로 아래의 하위 레이어만 의존하도록 설계해야 합니다.  
> 
> **사용자 인터페이스 레이어(Presentation Layer)**  
> 외부(웹 혹은 Event Queue 등)로부터 들어오는 요청을 응용 레이어(Application Layer)로 전달하는 역할을 하는 레이어입니다. 
> 기본적으로 수행해야 하는 폼 데이터 체크 및 파라미터 검증 등 유효성 처리 또한 사용자 인터페이스 레이어(Presentation Layer)에서 담당합니다.  
> Controller 혹은 Message Queue로 부터 메시지를 컨슘하는 EventListener가 이에 해당될 수 있습니다.    
> * 클라이언트의 요청을 받고 응답을 전달하는 역할을 합니다. (입출력 담당)
> * 클라이언트의 요청 데이터에 대한 유효성 검사를 합니다. (예: 필수 입력값 validation 체크)
> * 자원에 접근할 수 있는 권한을 검사합니다.
> * 사용자의 세션을 관리합니다.
> * Spring MVC가 이 표현 계층을 지원하는 대표적인 프레임워크입니다.
> * 클라이언트에서 온 요청 데이터를 응용 계층에서 지원하는 형식으로 변환하여 응용 계층에 전달하고 응답 데이터를 클라이언트가 지원하는 형식으로 변환하여 
> 클라이언트에게 전달 합니다. (예: HTTP 메시지를 요청 받아, 객체로 변환하여 응용 계층에 전달하고 다시 HTTP 응답 메시지로 변환하여 클라이언트에게 전달합니다.)  
> 
> **응용 레이어(Application Layer)**  
> 사용자 인터페이스 레이어로부터 메시지를 받아 요청에 맞는 비즈니스 로직을 수행하는 레이어입니다.  
> 도메인 모델을 이용해서 사용자에게 제공할 기능을 구현하게 되고, 실제 도메인 로직은 도메인 레이어에 위임하게 됩니다.  
> Service가 이에 해당될 수 있습니다.    
> Application Layer에 포함하는 기능들  
> * 응용 계층은 도메인 모델을 이용하여 클라이언트에게 제공할 기능을 구현합니다.
> * 비즈니스 로직 수행은 도메인 모델에 위임합니다.
> * 도메인 객체간의 실행 흐름을 제어합니다.
> * 도메인 모델의 정합성(논리적 오류)을 검증합니다. (예: 아이디 중복 여부 validation 체크)
> * 트랜잭션을 관리합니다.
> * 각 계층을 연결하여 각 계층이 지원하는 모델로 객체를 변환합니다. (예: dto -> 도메인, 도메인 -> dto)
> * 외부 모듈을 사용합니다. (예: 이메일 전송)
> * 도메인 이벤트를 처리합니다. (이벤트 핸들러) 
> 
> **도메인 레이어(Domain Layer)**  
> 도메인 레이어는 핵심 도메인 로직을 수행하는 레이어로 `엔티티`와 `Value Object`로 구성되어 있습니다.  
> 비즈니스 규칙, 정보에 대한 실질적인 도메인에 대한 정보를 가지고 있으며 이 모든 것을 책임지는 계층이다. 
> Entity를 활용하여 도메인 로직이 실행되며, 업무 상황을 반영하여 상태를 제어하는 역할에 집중하는 계층이다.  
> * 도메인 모델을 구현합니다.
> * 핵심 로직, 비즈니스 로직을 구현합니다. (정책, 비즈니스 규칙을 구현)
> * 도메인 이벤트를 발생시킵니다.
> 
> **인프라스트럭처 레이어(Infrastructure Layer)**  
> 외부와의 통신(DB, 메시징 시스템 등)을 담당하는 계층이다.  
> 해당 계층에서 얻어온 정보를 응용 계층 또는 도메인 계층에 전달하는 것이 주 역할이다.   
> 사용자 인터페이스, 응용, 도메인 레이어가 아닌 오로지 인프라스트럭처 레이어에서 구현 기술을 사용하게 됩니다.  
> 
> **DIP(Dependency Inversion Principle) - 의존 역전 원칙**  
> DIP란? 저수준 모듈이 고수준 모듈에 의존하도록 하는 것.  
> 고수준 모듈: 의미 있는 핵심 기능을 제공하는 모듈(여기서는 응용 영역, 도메인 영역이 해당된다.)  
> 저수준 모듈: 고수준 모듈이 핵심 기능을 구현하기 위해 필요로하는 하위 기능을 구현한 모듈(여기서는 인프라 영역이 해당된다.)  
> 
> 고수준 모듈이 제대로 동작하려면 저수준 모듈을 사용해야합니다. 그런데 고수준 모듈이 저수준 모듈을 사용하면   
> 테스트가 어려워집니다. 인프라는 구현 기술들을 다루는 곳입니다. 그런데 응용 영역인 서비스에서 도메인을 저장하기 위해 마이바티스를 사용한다고 생각해봅시다. 
> 해당 서비스를 테스트하기 위해서는 마이바티스라는 기술 구현이 완성되어 있어야하고(물론 여기서는 외부 라이브러리이기 때문에 완성됨을 보장 받지만) 
> 마이바티스 설정들이 모두 완벽하게 되어 있어야합니다. 서비스 단위 테스트를 하려고 했을 뿐인데 마이바티스에 의존적이게 됩니다.  
> 
> 고수준 모듈이 저수준 모듈을 사용하면 또한 구현 방식을 변경하기 어려워집니다.    
> 이때 DIP 를 통해 인터페이스를 이용해서 저수준 모듈이 반대로 고수준 모듈을 의존하게 만듭니다.    
> 
> DIP를 이용하면 테스트시, 구현 객체에 직접 의존하지 않기 때문에 실제 구현객체가 없어도 Mock 프레임워크를 이용하여 테스트가 가능합니다. 
> 또한 테스트를 위한 구현객체의 설정도 필요하지 않습니다.
> 구현 방식을 변경할 때도 서비스의 코드를 변경할 필요가 없어집니다.
>
> **레이어드 아키텍처의 장점**  
> * 각 레이어를 loosely coupling 된 형태로 구축하면서, 각각 자신의 관심사에만 집중할 수 있다.  
> * 핵심 비즈니스 로직을 순수하게 유지함으로써 유지보수와 확장성 측면에서 이득을 얻을 수 있다.  
> * 각 레이어에 서로 다른 추상화 수준을 가진 상태와 행동을 위치시킴으로써 코드 재사용성을 높일 수 있다.  
> 
> **레이어드 아키텍처의 단점**  
> * 서비스가 커질수록 복잡도가 증가하여 확장성이 떨어진다.  
> * 레이어로 분리된 관심사 외에 다른 관심사가 생길 경우 패키지 분리 및 코드 배치가 어렵다.  
> 
> **Layered Architecture를 사용해야 하는 경우**  
> 작고 단순하며 확장성보다는 일관성을 가져가는 것이 목표인 어플리케이션이나 웹사이트에 적합하다.  
> 또한 단순성 및 구현 용이성으로 인해 어플리케이션 시작점으로 사용하기에 좋다.  
> 
> **참조사이트**  
> [DDD 레이어드 아키텍처에 대하여](https://velog.io/@wodyd202/DDD-%EB%A0%88%EC%9D%B4%EC%96%B4%EB%93%9C-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC)  
> [도메인 주도 설계의 계층화 아키텍처(Layered Architecture)와 DIP](https://yoonbing9.tistory.com/123)

### Clean 아키텍처
> 소프트웨어의 각 계층을 분리하여 의존성을 최소화하고 테스트 용이성을 향상시키는 것을 목표로한다.  
> Clean Architecture에 대해서 이해하기 위해선 두 가지 개념을 이해하고 있어야 합니다.  
> * Business Rule
> * System Architecture
> 
> **What is Business Rule?**  
> Business Rule(Logic)은 컴퓨터 프로그램에서 데이터를 생성, 표시, 저장, 변경하는 부분을 일컫습니다. (=domain logic)
> Business Rule(Logic)은 유저의 입력(UI)과 DB 사이에서 발생한 정보 교환을 위한 특정 알고리즘이나 규칙이 정의된 tier 를 의미합니다.  
> 이러한 Rule(Logic)은 고객의 요구에 따라 변경될 수 있기 때문에 별도의 tier 에 배치되어야 합니다. 만약 다른 역할을 하는 tier와 함께 존재한다면, 
> 고객의 요구에 따라 변경해야하는 부분이 많아질 수 밖에 없기 때문입니다.  
> 
> **What is System Architecture?**  
> System Architecture는 시스템의 구조(structure), 행위(behavior), 뷰(views)를 정의하는 개념적인 모델입니다.  
> 즉, 시스템의 목적을 달성하기 위해 각 컴포넌트가 어떻게 상호작용하고 정보가 어떻게 교환되는 지를 정의하고 있습니다.  
> 세상에는 정말 다양한 시스템 아키텍처들이 나왔지만 결국 그들의 목적은 하나로 귀결됩니다: 관심사의 분리  
> 
> **관심사의 분리**  
> 소프트웨어를 계층으로 나누게 되면 관심사를 분리할 수 있습니다. 그리고 관심사 분리에 목적을 가진 시스템 아키텍처는 최종적으로 다음과 같은 구조를 지니게 됩니다.  
> 프레임워크 독립적: 라이브러리 존재 여부나 프레임워크에 한정적이지 않아 도구로써 사용하는 것이 가능합니다.  
> 테스트 용이: Business Rule은 UI, DB, Web Server 등 기타 외부 요인과 관계없이 테스트 가능합니다.  
> UI 독립적: 시스템의 다른 부분을 고려하지 않고 UI를 변경할 수 있습니다.  
> Database 독립적: Business Rule에 얽매이지 않고 Database를 독립적으로 변경할 수 있습니다(SQL, Mongo, CouchDB 등)  
> 외부 기능 독립적: Business Rule은 외부 상황(DB, UI)이 변하더라도 영향을 받지 않습니다.  
>
> **Domain**  
> Domain Layer는 Business Rule이 존재하는 영역입니다. 번역앱은 번역을 하고, 결제 앱은 결제를 수행합니다. 
> 이렇듯 비즈니스의 본질은 쉽게 바뀌지 않으므로 Business Rule은 잘 변하지 않는 안정된 영역입니다.  
> 
> **Infrastructure**  
> Infrastructure Layer는 UI, Database, Web APIs, Frameworks 등이 존재하는 영역입니다. 이는 Domain에 비하여 자주, 쉽게 바뀔 수 있습니다. 
> 예를 들어 다른 사용자에게 송금을 한다고 가정해봅시다. 송금을 위한 버튼의 형태는 쉽게 바뀔 수 있지만 송금 방법 (Business Rule)은 그렇지 않습니다.  
> Uncle Bob은 이렇게 경계를 두어 각 Layer를 분리하고, 관심사를 분리하는 규칙을 의존성 규칙(Dependency Rule)으로 설명했습니다.  
> 
> **Dependency Rule**  
> 모든 소스코드 의존성은 반드시 outer(저수준) 에서 inner(고수준) 로, 고수준 정책을 향해야 한다.  
> Dependency Rule은 Business Logic을 담당하는 코드들이 DB 또는 Web 같이 구체적인 세부사항에 의존하지 않고 독립적으로 실행되어야 한다는 규칙입니다.  
> Dependency Rule에 따르면 inner circle에 해당하는 Domain은 outer circle에 해당하는 Infrastructure에 대해서 아무것도 모릅니다. 
> 이는 UI, DB는 Business Rule에 의존하지만 Business Rule은 그렇지 않다는 것을 의미합니다.  
> UI가 웹이건 모바일이건, DB가 SQL이건 NoSQL이건 Business Rule 입장에선 아무런 관계가 없습니다.  
> Domain이 Entities, Use Cases로 세분화 되었고, Adapter가 새로 생겨 Domain과 Infrastructure 사이의 경계를 관리합니다.  
> Dependency Rule에 따라 동작하여 outer에서 inner로 의존성을 가지게 됩니다.  
> 
> **Entity**  
> Entity는 애플리케이션에서 핵심적인 기능인 Business Rule을 담고 있습니다.  
> 다른 사람에게 돈을 보내는데, 같은 은행으로 보내면 수수료가 면제된다고 가정해 보겠습니다. 
> 모바일 앱에서 돈을 보내던 PC 웹에서 돈을 보내던 같은 은행으로 보내면 수수료가 면제된다는 사실은 변하지 않습니다.  
> 같은 은행이면 수수료가 면제된다는 규칙(Business Rule)은 외부 상황(outer layer)을 전혀 모릅니다.  
> 즉, Entity들은 outer layer들에 속한 다른 class나 component들을 전혀 모르고 신경쓰지 않아도 됩니다.  
> 
> **Use cases**  
> Use cases는 특정 application에 대한 Business Rule입니다. Use cases는 시스템이 어떻게 자동화 될 것인지에 대해 정의하고 application의 행위를 결정합니다. 
> 다시 말해, 프로젝트 레벨의 Business Rules(Entities)을 사용하여 Use cases의 목적을 달성합니다.  
> 계좌 송금을 하기 위한 Use cases의 예시는 다음과 같습니다.  
> [계좌 송금]  
> * 입력: 수취인 계좌번호, 수취인 은행, 송금 금액
> * 출력: 송금 성공 여부
> * 적용되는 Business Rule:  
> 계좌번호의 양식은 유효해야 한다.  
> 해당 계좌가 돈을 수취할 수 있는 유효한 상태여야 한다.  
> 송금 금액은 1회에 1천만원까지만 허용된다.  
> ...  
> 
> Use cases 는 Entities에 의존하는 동시에 상호작용합니다. 물론 outer layer에 대해서는 아는게 없습니다. 
> 다만 이 계층에서는 outer layer에서 사용할 수 있는 abstract class나 interface를 정의합니다.  
> 
> **Adapters**  
Adapters는 domain과 interfaces 사이의 번역기 역할을 수행합니다.
> 예를 들어 GUI로부터 input data를 받아 Use cases와 Entities 에게 편리한 형태로 repackage 하고, 
> Use cases와 Entities의 output을 가져와 GUI에 표시하거나 DB에 저장하기 편리한 형식으로 repackage 합니다.  
> Adapters는 GUI의 MVC 아키텍처를 완전히 내포하며, `Presenter`, `View`, `Controller` 가 모두 여기에 속합니다.  
>  
> **Infrastructure**  
> Infrastructure는 모든 I/O components(UI, DB, Frameworks, Devices)가 있는 영역입니다.  
> 이는 변화될 가능성이 매우 높기 때문에 stable 한 domain과는 확실히 분리가 되어 있고, 그렇기 때문에 비교적 쉽게 변화되고 component 또한 쉽게 교환됩니다.  
> 
> **Conclusion**  
> 결국 Clean Architecture는 다음과 같은 이점이 있다고 정의내립니다.  
> * 의존성 규칙에 따름으로써 관심사가 분리된다.  
> * 본질적으로 테스트하기 쉬운 시스템을 만들 수 있다.  
> * 의존성 규칙이 가져오는 이점을 가져올 수 있다.  
> * 그리고 주요한 이러한 특징을 지닙니다.  
> 
> 또한 같은 상황과 이유로 변경되는 Class들은 Components로 묶인다.
> Business Rule은 stable한 components로, 변경되기 쉬운 외부의 infrastructure components (UI, DB, web, frameworks, ... )를 알지 못한다.
> 각 components layer 간의 경계는 adapter 인터페이스를 통해 관리된다.
> Adapter는 Layer 간의 데이터를 편한 형태로 변환시켜주고 더 stable한 inner components로 의존성을 가지도록 한다.  
> 
> **단점**  
> 클린 아키텍처는 공짜가 아니고, 실제로 구현해보면 다양한 대가를 치러야만 한다는 걸 느낄 수 있습니다.  
> 의존성에 대한 엄격한 규칙 때문에, 각 계층에서 사용해야 할 모델을 만들어주고 그것을 계층마다 변환해주는 매핑 작업이 필요합니다.  
> 추상화된 인터페이스와 다양한 구현체를 만들어 주는 것, 서비스를 여러 개의 작은 유스케이스로 분리해보는 경험에서 감당할 수 있는 범위 이상의 클래스 개수를 만날 수 있습니다.  
> 이 아키텍처에서는 JPA에서 사용하던 엔티티 클래스를 도메인 계층에 포함할 수 없습니다. 영속성에 대한 여러 제약사항이 클래스에 포함되니까요. 
> 이러한 경우에서는 도메인 계층에서 사용하는 엔티티와 영속성 계층에서 사용하는 엔티티를 분리해줘야 합니다.  
>
> **참조사이트**  
> [Why DDD, Clean Architecture and Hexagonal ?](https://dataportal.kr/74)

### Hexagonal 아키텍처
> 헥사고날 아키텍처는 전통적인 계층형 아키텍처의 단점을 보완하기 위해 생겼다.
> 도메인 중심 아키텍처의 일종으로 클린 아키텍처를 일반화한 구조 중 하나이다. (포트와 어댑터(Ports and Adapters) 아키텍처라고도 말한다.)
>
> **계층형 아키텍처의 단점 1.전통적인 계층형 아키텍처의 도메인 계층은 영속성에 의존한다.**    
> 즉, 도메인 계층이 자연스레 데이터 베이스에 의존하게 되어서 데이터 베이스에 변화가 일어난다면 도메인 계층도 변화가 생긴다.    
> 추가로 서비스 계층에서도 영속성 모델(JPA Entity)을 도메인 모델 처럼 사용하게 된다.    
> 결과적으로 해당 도메인 모델을 사용하는 서비스 계층에서도 즉시 로딩, 지연 로딩, 트랜잭션, 플러시 등을 고려해야 하고, 영속성에 대한 의존이 프로젝트 전체적으로 퍼지게 되고 변경에 취약해진다.
>
> **계층형 아키텍처의 단점 2.아키텍처 경계를 강제할 수 없다.**  
> 전통적인 계층형 아키텍처에서는 상위 계층에 있는 컴포넌트를 접근할 목적으로 해당 컴포넌트를 하위 계층으로 내려버릴 수 있다.
> 해당과 같은 행위가 쌓이면, 점점 경계가 모호해지다가 결국 경계가 허물어지게 된다.   
> 중요한 것은 부적절한 선택지를 닫아야 한다는 점이다. 선택지가 열려 있으면 누군가는 반드시 그렇게 하기 마련이다.
>
> **계층형 아키텍처의 단점 3.계층을 Skip 할 수 있다.**  
> 계층형 구조에서 많이 나타나는 형태로 계층을 건너뛰는 것이 가능하다. 가령, 구현이 간단한 경우 Controller에서 바로 도메인을 참조해서 로직을 작성할 수 있다.    
> 이 경우 첫 번째 문제는 기능이 확장이다. '기능이 추가되면 해당 로직을 서비스 계층으로 로직을 옮기겠지..?' 라고 생각하지만, 다른 동료는 그렇게 생각하지 않을 수 있다.  
> 두 번째 문제는 테스트가 복잡해진다는 것이다. Controller가 Application Layer를 건너뛰어서 영속성 리포지토리에 바로 접근하는 경우가 있다고 가정한다.  
> 그러면 Controller의 단위 테스트를 하는데 영속성 계층도 Mocking을 하면서 복잡한 처리를 해야만 테스트가 가능하게 된다.
>
> **계층형 아키텍처의 단점 4.유스케이스를 숨긴다.**  
> 개발자들은 새로운 유스케이스를 구성하는 새로운 코드를 짜는 것을 선호하지만, 실제로는 기존 코드를 바꾸는 데 더 많은 시간을 소모한다. 유스케이스 로직의 존재 여부, 적절한 위치 등을 파악 등.  
> 개발자는 유스케이스를 웹 계층에도 생성할 수 있고, 영속성 계층에도 생성할 수 있고 자유롭다.  
> 즉, 개발자가 해당 유스케이스가 존재하는 지 여부를 파악하기 어려워서 동일한 로직을 다른 위치에 새롭게 구현하여 코드를 더럽힐 수 있게 된다.
>
> **계층형 아키텍처의 단점 5.서비스의 크기를 강제할 수 없다.**  
> 계층형 구조에서는 서비스의 크기를 강제하지 않는다. 그래서 PostService에 수십개의 서비스 로직을 전부 때려박는 것도 가능해진다.  
> 이 경우 Service는 너무 많은 의존을 가져버리고, 수많은 Web 계층이 해당 Service를 의존하게 된다.  
> 결국 서비스를 테스트하기 어려워지고 작업해야 할 유즈케이스를 찾기도 힘들어진다.
>
> **헥사고날 아키텍처**  
> 헥사고날 아키텍처(육각형 아키텍처)는 알레스테어 콕번이 만든 용어로 클린 아키텍처를 일반화한 구조 중 하나이다.  
> (육각형 모양은 사실 아무 의미가 없다. 애플리케이션이 다른 시스템이나 어댑터와 연결되는 4개의 면을 나타내기 위해 육각형을 사용했다고 한다.)  
> 헥사고날 아키텍처에서는 사용자 인터페이스나 데이터베이스 모두 비즈니스 로직으로부터 분리해야 하는 외부 요소로 취급한다.  
> 이는 비즈니스 로직이 외부 요소에 의존하지 않고 프레젠테이션 계층과 데이터 소스 계층이 도메인 계층에 의존하도록 만들어야 한다는 것이다.  
> 
> 육각형 안에는 도메인 엔터티와 이와 상호작용하는 비즈니스 로직(UseCase)가 있다. 이는 육각형 외부로 향하는 의존성이 없기 때문에 클린 아키텍처에서 제시한 의존성 규칙이 그대로 적용된다. 모든 의존성은 코어를 향한다.
> 서론에서 헥사고날 아키텍처는 포트와 어댑터 아키텍처로 부르기도 한다고 했다. 육각형 바깥에는 애플리케이션과 상호작용하는 어댑터가 있다. 일부 어댑터는 외부 시스템과 상호작용하며, 데이터베이스와 상호 작용하는 어댑터도 있다.  
> 왼쪽에 있는 어댑터는 애플리케이션 코어를 호출하는 어댑터이고, 오른쪽에 있는 어댑터는 애플리케이션 코어에 의해 호출되는 어댑터이다.  
> 어댑터와 애플리케이션 코어 간 통신을 할 때는 각각의 포트를 사용해야 한다.    
> 클린 아키텍처와 헥사고날 아키텍처 모두 의존성을 역전시켜 도메인 코드가 바깥쪽 코드에 의존하지 않게 함으로써 외부로 부터의 도메인 로직의 결합을 제거한다. 
> 변경할 이유가 적을수록 유지보수성이 높은 코드가 된다.   
> 
> **Domain Objects**  
> 비즈니스 규칙이 풍부한 도메인에서 도메인 객체는 애플리케이션의 생명입니다. 도메인 객체는 상태(state)와 동작(behavior)을 모두 포함할 수 있습니다. 
> 동작과 상태가 가까이 있을수록 코드를 더 쉽게 이해하고 유추하고 유지 관리할 수 있습니다.  
> 도메인 객체에는 외부로 향하는 종속성이 없습니다. 그것들은 순수한 코드 덩어리이며 유즈 케이스가 도메인 객체를 조작(operate)할 수 있도록 API를 제공합니다.  
> 도메인 객체는 응용 프로그램의 다른 계층에 의존하지 않으므로 다른 계층의 변경 사항이 도메인 객체에 영향을 미치지 않습니다. 종속성 없이 발전할 수 있습니다. 
> Single Responsibility Principle(“SOLID"의 “S”)의 대표적인 예입니다. 도메인 객체가 변경되는 이유는 비즈니스 요구 사항의 변경입니다.  
> 단일 책임을 가짐으로써 외부 종속성을 고려할 필요 없이 도메인 객체를 발전시킬 수 있습니다. 이러한 발전 가능성은 도메인 주도 설계를 적용할 때 육각형 아키텍처 스타일을 
> 완벽하게 만들어줍니다. 개발하는 동안 우리는 종속성의 자연스러운 흐름을 따릅니다: 우리는 도메인 객체에서 코딩을 시작하고 거기에서 바깥쪽으로 나아갑니다.  
> 
> **Use Cases**  
> [[Hexagonal Architecture] 헥사고날 아키텍처에서 유즈케이스(UserCase) 구현하기](https://velog.io/@msung99/Hexagonal-Architecture-%ED%97%A5%EC%82%AC%EA%B3%A0%EB%82%A0-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98%EC%97%90%EC%84%9C-%EC%9C%A0%EC%A6%88%EC%BC%80%EC%9D%B4%EC%8A%A4UserCase-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)
> 
> **Inbound and Outbound Ports**  
> 도메인 객체 및 유즈 케이스는 육각형 내에 있습니다. 즉, 애플리케이션의 핵심 내에 있습니다. 외부와의 모든 통신은 전용 "포트"를 통해 이루어집니다.    
> Inbound 포트는 외부 구성 요소에서 호출할 수 있고 유즈 케이스에 의해 구현되는 간단한 인터페이스입니다. 이러한 Inbound 포트를 호출하는 구성 요소를 Inbound 어댑터라고 합니다.    
> Outbound 포트는 외부에서 무언가가 필요한 경우(예: 데이터베이스 액세스), 유즈 케이스에서 호출할 수 있는 간단한 인터페이스입니다.   
> 이 인터페이스는 유즈 케이스의 요구 사항에 맞게 설계되었지만 Outbound 어댑터라고 하는 외부 구성 요소에 의해 구현됩니다.     
> SOLID 원칙에 익숙하다면 인터페이스를 사용하여 유즈 케이스에서 Outbound 어댑터로 종속성의 방향을 반전시키기 때문에 이것은 Dependency Inversion Principle(SOLID의 “D”)의 적용입니다.    
> Inbound 및 Outbound 포트가 있으면, 데이터가 시스템에 들어오고 나가는 위치가 매우 뚜렷하므로 아키텍처에 대해 쉽게 추론할 수 있습니다.  
> 
> **Adapters**    
> 어댑터는 육각형 아키텍처의 외부 레이어를 형성합니다. 어댑터들은 코어의 일부가 아니지만 코어와 상호작용합니다.  
> Inbound 어댑터는 Inbound 포트를 호출하여 작업을 수행합니다. 예를 들어 Inbound 어댑터는 웹 인터페이스가 될 수 있습니다.   
> 사용자가 브라우저에서 버튼을 클릭하면 웹 어댑터가 특정 Inbound 포트를 호출하여 해당 유즈 케이스를 호출합니다.  
> Outbound 어댑터는 유즈 케이스에 따라 호출되며 예를 들어 데이터베이스의 데이터를 제공할 수 있습니다. Outbound 어댑터는 Outbound 포트 인터페이스의 집합을 구현합니다.   
> 인터페이스는 유즈 케이스에 따라 결정되며 그 반대로 구현해서는 안됩니다.  
> 어댑터를 사용하면 응용 프로그램의 특정 계층을 쉽게 교체할 수 있습니다. 응용 프로그램을 웹에 추가로 팻 클라이언트에서 사용할 수 있어야 하는 경우 팻 클라이언트 Inbound 어댑터를 추가합니다.   
> 응용 프로그램에 다른 데이터베이스가 필요한 경우 이전 것과 동일한 Outbound 포트 인터페이스를 구현하는 새 영속성 어댑터를 추가합니다.  
> 
> 어댑터는 크게 2종류로 구분됩니다.  
> * Driving Adapter : 애플리케이션의 코어(도메인, 엔티티등) 을 호출하는 엔티티. 즉 웹 어댑터가 이에 해당합니다.  
> * Driven Adapter : 애플리케이션에 의해 주도되는 어댑터들입니다. 즉 영속성 어댑터가 이에 해당하죠.  
> 
> [[Hexagonal Architecture] 헥사고날 아키텍처에서 인커밍 웹 어댑터(Adapter) 를 컨트롤러로 구현하기](https://velog.io/@msung99/Hexagonal-Architecture-%ED%97%A5%EC%82%AC%EA%B3%A0%EB%82%A0-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98%EC%97%90%EC%84%9C-%EC%9D%B8%EC%BB%A4%EB%B0%8D-%EC%96%B4%EB%8C%91%ED%84%B0Adapter-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)
> 
> **접근 제한자**  
> 패키지의 수가 아주 많아진다는 것이 모든 것을 public 으로 만들어서 패키지 간의 접근을 허용해야 한다는 것은 아닐까? 걱정스럽다.  
> 하지만 그렇지 않다! 이 패키지에 들어 있는 모든 클래스 들은 application 패키지 내에 있는 포트 인터페이스를 통하지 않고는 바깥에서 호출될 수 없다.   
> 그래서 모든 어댑터를 package-private(Java 기준 default) 접근 수준으로 둘 수 있다.  
> 이러한 구조는 애플리케이션 계층에서 어댑터 계층으로 향하는 의존을 막는다!  
> 
> **Pros**  
> 유지보수성    
> 관심사를 분리하고 비즈니스 로직 디커플링을 제공하여 수정하고자 하는 코드를 쉽게 찾을 수 있기 때문에 유지보수 가능성을 높입니다.  
> 
> 유연함  
> 서로 다른 기술 간의 교환은 쉽습니다. 지정된 포트에 대해 각각 특정 기술을 사용하는 여러 개의 어댑터를 가질 수 있습니다. 
> 둘 중 하나를 선택하려면 해당 포트에 사용할 어댑터를 구성하기만 하면 됩니다. 이 구성은 외부 구성 속성 파일을 수정하는 것만큼 쉽습니다. 소스 코드 수정, 재컴파일, 재작성도 없습니다.  
> 마찬가지로 기존 소스 코드를 건드리지 않고도 포트에 특정 기술 어댑터를 새로 추가할 수 있습니다. 어댑터는 따로 개발 및 컴파일됩니다. 런타임에 의존성이 주입되어 포트에 연결됩니다.  
> 
> 기술 발전에 영향을 받지 않는 애플리케이션  
> 기술은 비즈니스 로직보다 더 자주 발전합니다. 비즈니스 로직이 기술에 묶여 있는 애플리케이션에서는 비즈니스 로직에 손을 대지 않고는 기술 변화를 수행할 수 없습니다. 
> 비즈니스 로직이 바뀌면 순간 애플리케이션의 모든 코드들은 불안정한 상태로 변하게 됩니다.  
> 육각형 아키텍처에서 업그레이드하려는 기술은 애플리케이션 외부의 어댑터에 있기 때문에 어댑터만 교체하면 됩니다. 도메인은 어댑터에 의존하지 않기 때문에 애플리케이션 자체는 변하지 않습니다.  
> 
> 기술적 의사 결정 연기  
> 개발과 코딩을 시작할 때 어떤 프레임워크와 기술을 사용할지 결정을 미루고 비즈니스 로직에만 집중할 수 있습니다. 나중에 기술을 선택하고 어댑터를 코딩할 수 있습니다.  
> 
> 테스트 기능 향상  
> 이 아키텍처가 제공하는 주요 이점은 의존적인 외부 장치로부터 애플리케이션을 격리하여 테스트할 수 있다는 것입니다. 이 작업은 다음 두 가지 작업을 통해 수행할 수 있습니다.  
> 각 포트에 대해 포트에 대한 테스트 사례를 실행할 테스트 어댑터를 개발합니다.  
> 각 포트에 대해 mock 어댑터를 개발합니다.  
> 
> **Cons**  
> 복잡성  
> 육각형 아키텍처를 구현하는 소프트웨어 프로젝트는 복잡한 구조를 가지고 있으며, 이들 사이에 많은 모듈과 명시적인 의존성이 정의되어 있습니다.  
> 
> 애플리케이션 생산성  
> 방금 살펴본 복잡성으로 인해, 프로젝트가 너무 크고 어댑터가 많다면, 컴파일하고 테스트를 실행하고, 모든 모듈을 함께 만들고, 전체 프로젝트를 시작하는 과정에는 많은 시간이 걸릴 것입니다.
> 
> 맵핑 객체들  
> 포트 및 어댑터를 통해 기술과 애플리케이션을 분리하면 간접적으로, 즉 어댑터가 포트와 특정 기술 인터페이스 간에 변환될 때 메소드에 대한 추가 호출이 추가됩니다. 
> 그 외에도 응용 프로그램과 외부 객체 간의 매핑이 필요할 수 있습니다.  
>  
> **결론**  
> 단순히 데이터를 저장하고 읽는 CRUD 애플리케이션을 구축하는 경우 이와 같은 아키텍처는 아마도 오버헤드일 것입니다.   
> 하지만 상태와 동작을 결합하는 풍부한 도메인 모델로 표현할 수 있는 풍부한 비즈니스 규칙으로 애플리케이션을 구축하는 경우, 
> 이 아키텍처는 도메인 모델을 요소들의 중심에 배치하기 때문에 정말 많은 효과를 볼 수 있을 겁니다.  
> 
> **참조사이트**  
> [헥사고날(Hexagonal) 아키텍처란 무엇인가?!](https://jaehoney.tistory.com/313)    
> [DDD + Hexagonal Architecture(WITH 글로벌 프로젝트)](http://dev.blog.sellmate.co.kr/post/%EA%B8%80%EB%A1%9C%EB%B2%8C-5%EC%B0%A8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%A6%AC%EB%B7%B0/)    
> [스프링 코드로 이해하는 핵사고날 아키텍처](https://covenant.tistory.com/258)    
> [[Hexagonal Architecture] 헥사고날 아키텍처로 어떻게 유지.보수 가능한 소프트웨어를 개발할까?](https://velog.io/@msung99/Hexagonal-Architecture-%ED%97%A5%EC%82%AC%EA%B3%A0%EB%82%A0-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98%EB%A1%9C-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9C%A0%EC%A7%80.%EB%B3%B4%EC%88%98-%EA%B0%80%EB%8A%A5%ED%95%9C-%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4%EB%A5%BC-%EA%B0%9C%EB%B0%9C%ED%95%A0%EA%B9%8C)  
> [[Hexagonal Architecture] 헥사고날 아키텍처에서 유즈케이스(UserCase) 구현하기](https://velog.io/@msung99/Hexagonal-Architecture-%ED%97%A5%EC%82%AC%EA%B3%A0%EB%82%A0-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98%EC%97%90%EC%84%9C-%EC%9C%A0%EC%A6%88%EC%BC%80%EC%9D%B4%EC%8A%A4UserCase-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)  

---

## 경계 간 매핑 전략
### 개요
> 클린 아키텍처 및 그것을 구체화한 헥사고날 아키텍처에서는 웹, 애플리케이션, 도메인, 영속성 계층이 존재하고 각 계층에서 같은 모델을 사용할지 다른 모델을 사용할 지에 대해서 다룬다.  
> 각 계층에서 다른 모델을 사용할 경우 도메인에서 사용하는 모델과 유스케이스로 출력하는 모델이 달라진다. 이럴 때 도메인 사용 모델을 유스케이스 출력 모델로 변환하는 과정을
> 매핑이라 한다.  
> 
> 매핑을 필요하다는 의견과 필요없다는 의견이 존재한다.    
> * 매핑이 필요하다는 의견: 두 계층 간에 매핑을 하지 않으면 양 계층에서 같은 모델을 사용해야 하는데 이렇게 하면 두 계층이 강하게 결합된다.
> * 매핑이 필요없다는 의견: 하지만 두 계층 간에 매핑을 하게 되면 보일러플레이트 코드를 너무 많이 만들게 된다. 많은 유스케이스들이 오직 CRUD 만 수행하고
> 계층에 걸쳐 같은 모델을 사용하기 때문에 계층 사이의 매핑은 과하다.  
> 
> 두 의견 모두 맞는 부분이 있다. 개발자들이 매핑을 어떤 방식으로 구현할 수 있는지에 대한 전략들을 아래에 설명한다.  

### '매핑하지 않기' 전략
> 웹 계층 -> 유스케이스 <- 서비스(유스케이스 구현) -> 아웃고잉 포트 <- 영속성 어댑터  
> 여기서 유스케이스의 출력과 서비스에서 사용하는 도메인 객체, 아웃고잉 포트로 내보내거나 가져오는 모델까지 모두 같은 모델 클래스를 사용하게 되면 따로 맵핑이 필요가 없다.  
> 
> 만약 웹 계층에서도 같은 모델을 응답으로 출력하게 되면 해당 모델에는 JSON 으로 직렬화하기 위한 애너테이션을 필드에 붙여야할 수 있게 되며,
> 영속성 계층에서도 같이 사용하게 되면 JPA 관련 애노테이션도 붙여야하게 된다.  
> 도메인과 애플리케이션 계층은 웹이나 영속성과 관련된 특수한 요구사항에는 관심이 없음에도 불구하고 해당 모델 클래스는 이런 모든 요구사항을 다뤄야 한다.  
> 해당 모델 클래스는 웹, 애플리케이션, 영속성 계층과 관련된 이유로 인해 변경돼야 하기 때문에 객체를 변경할 때는 한 가지 이유만 있어야한다는 `단일 책임 원칙`에 위배된다.  
> 
> 또한 기술적인 요구사항이 아니더라도, 각 계층이 모델 클래스에 특정 커스텀 필드를 두도록 요구할 수도 있다. 그 결과, 오로지 한 계층에서만 필요한 필드들을 포함하는 파편화된
> 도메인 모델로 이어질 수 있다.  
> 
> 하지만 '매핑하지 않기' 전략에 딱 들어맞는 경우가 있다. 바로 간단한 CRUD 유스케이스를 구현하는 경우이다.  
> 모든 계층이 정확히 같은 구조의, 정확히 같은 정보를 필요로 한다면 '매핑하지 않기' 전략은 완벽한 선택지다.  
> 그러나 간단한 CRUD 유스케이스로 시작해서 시간이 지남에 따라 값비싼 매핑 전략이 필요한, 풍부한 행동과 유효성 검증을 가진 제대로 된 비즈니스 유스케이스가 필요해지면
> 곧바로 다른 전략을 취해야 한다.  

### '양방향' 매핑 전략
> 웹 계층에서는 웹 모델을 유스케이스에서 필요한 도메인 모델로 매핑하고, 유스케이스에 의해 반환된 도메인 객체를 다시 웹 모델로 맵핑한다.  
> 영속성 계층은 아웃고잉 포트가 사용하는 도메인 모델과 영속성 모델 간의 매핑과 유사한 매핑을 담당한다.  
> 
> 두 계층 모두 양방향으로 매핑하기 때문에 '양방향' 매핑이라고 부른다.  
> 
> 각 계층이 전용 모델을 가지고 있는 덕분에 각 계층이 전용 모델을 변경하더라도 다른 계층에는 영향이 없다. 그래서 웹 모델은 데이터를 최적으로 표현할 수 있는 구조를
> 가질 수 있고, 도메인 모델은 유스케이스를 제일 잘 구현할 수 있는 구조를 가질 수 있다.  
> 이 매핑 전략은 웹이나 영속성 관심사로 오염되지 않은 깨끗한 도메인 모델로 이어진다. JSON 이나 ORM 매핑 애너테이션이 없어도 된다. 단일 책임 원칙을 만족하는 것이다.  
> 
> 다른 매핑 전략과 마찬가지로 '양방향' 매핑도 단점이 있다.  
> 먼저, 너무 많은 보일러플레이트 코드가 생긴다.  
> 또 이 전략은 유스케이스 및 아웃고잉 포트가 도메인 객체를 반환 값 및 입력 파라미터로 사용한다. 도메인 모델은 도메인 모델의 필요에 의해서만 변경되는 것이 이상적이지만
> 바깥쪽 계층의 요구에 따른 변경에 취약해지는 것이다.  

### '완전' 매핑 전략
> 완전 매핑 전략에서는 각 연산마다 별도의 입출력 모델을 사용한다. 계층 경계를 넘어 통신할 때 도메인 모델을 사용하는 대신 유스케이스의 입력 모델로 XXXCommand 와 같은
> 이름의 DTO 를 따로 사용한다. 이런 DTO 는 `command` 혹은 `request` 와 비슷한 단어로 표현한다.  
> 
> 웹 계층은 입력을 애플리케이션 계층의 커맨드 객체로 매핑할 책임을 가지고 있다. 이러한 커맨드 객체는 애플리케이션 계층의 인터페이스를 해석할 여지 없이 명확하게
> 만들어 준다. 어떤 필드를 채울지, 어떤 필드를 비워두는게 나은지 추측할 필요가 전혀 없는데, 값을 비워둘 수 있는 필드를 허용할 경우에는 현재의 유스케이스에서는 필요없는
> 유효성 검증이 수행될 수도 있기 때문이다.  
> 
> 그리고 나서 애플리케이션 계층은 커맨드 객체를 유스케이스에 따라 도메인 모델을 변경하기 위해 필요한 무엇인가로 매핑할 책임을 가진다.  
> 이 매핑 전략을 전역 패턴으로 추천하지는 않는다. 이 전략은 웹 계층(혹은 인커밍 어댑터 종류 중 아무거나)과 애플리케이션 계층 사이에서 상태 변경 유스케이스의
> 경계를 명확하게 할 때 가장 빛을 발한다.  
> 애플리케이션 계층과 영속성 계층 사이에서는 매핑 오버헤드 때문에 사용하지 않는 것이 좋다.  
> 또한 어떤 경우에는 연산의 입력 모델에 대해서만 이 매핑을 사용하고(Command 객체 사용), 도메인 객체를 그대로 출력 모델로 사용하는 것도 좋다.  
> 이처럼 매핑 전략은 여러 가지를 섞어쓸 수 있고, 섞어 써야만 한다. 어떤 매핑 전략도 모든 계층에 걸쳐 전역 규칙일 필요가 없다.  

### '단방향' 매핑 전략
> 이 전략에서는 모든 계층의 모델들이 같은 인터페이스를 구현한다. 이 인터페이스는 관련 있는 특성(attribute)에 대한 getter 메서드를 제공해서 
> 도메인 모델의 상태를 캡슐화한다.  
> 도메인 모델 자체는 풍부한 행동을 구현할 수 있고, 애플리케이션 계층 내의 서비스에서 이러한 행동에 접근할 수 있다. 도메인 객체를 바깥 계층으로 전달하고 싶으면
> 매핑 없이 할 수 있다. 왜냐하면 도메인 객체가 인커밍/아웃고잉 포트가 기대하는 대로 상태 인터페이스를 구현하고 있기 때문이다.  
> 행동을 변경하는 것이 상태 인터페이스에 의해 노출돼 있지 않기 때문에 실수로 도메인 객체의 상태를 변경하는 일은 발생하지 않는다.  
> 
> 바깥 계층에서 애플리케이션 계층으로 전달하는 객체들도 이 상태 인터페이스를 구현하도록 할 수도 있다.  
> 
> 이 전략은 계층 간의 모델이 비슷할 때 가장 효과적이다. 예를 들어, 읽기 전용 연산의 경우 상태 인터페이스가 필요한 모든 정보를 제공하기 때문에 
> 웹 계층에서 전용 모델로 매핑할 필요가 전혀 없다.  



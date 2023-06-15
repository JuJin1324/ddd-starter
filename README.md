# ddd-starter

## 패키지
### 패키지 관리
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
> 

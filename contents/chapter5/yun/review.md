# 5장 서비스 추상화

구현 예제의 정리는 생략합니다. 그래서 정리 내용이 굉장히 짧습니다.

## 서비스 추상화와 단일 책임 원칙
* 애플리케이션 로직의 종류에 따른 수평적인 구분이든, 로직과 기술이라는 수직적인 구분이든 모두 결합도가 낮으며, 서로 영향을 주지 않고 자유롭게 확장될 수 있는 구조를 만들 수 있는 데는 스프링의 DI가 중요한 역할을 하고 있다.
* DI의 가치는 관심, 책임, 성격이 다른 코드를 깔끔하게 분리하는 데 있다.

#### 단일 책임 원칙
* 하나의 모듈은 한 가지 책임을 가져야 하며 모듈이 바뀌는 이유는 한 가지여야 한다.
* 단일 책임 원칙을 이행하면 수정 대상이 명확해진다.
* 애플리케이션 로직과 기술/환경을 분리하는 등의 작업의 핵심적인 도구가 DI다.
* 객체지향 설계와 프로그래밍의 원칙은 서로 긴밀하게 관련이 있다.

#### 단일 책임 원칙을 잘 지키는 코드
* 인터페이스를 도입하고 이를 DI로 연결한다.
* 단일 책임 원칙뿐 아니라 개방 폐쇄 원칙도 잘 지킨다.
* 모듈 간의 결합도가 낮아서 서로의 변경이 영향을 주지 않는다.
* 같은 이유로 변경이 단일 책임에 집중되는 응집도 높은 코드를 만든다.
* 디자인 패턴이 자연스럽게 적용된다.
* 테스트가 편하다.

#### DI
* 스프링을 DI 프레임워크라고 부르는 이유는 스프링이 DI에 담긴 원칙과 이를 응용하는 프로그래밍 모델을 적극 활용하고, 깔끔하고 유연한 코드와 설계를 만들어낼 수 있도록 지원하기 때문이다.
* DI를 공부하다보면 객체지향 원칙과 디자인 패턴의 장점이 잘 녹아 있다는 사실을 발견하게 된다.

## 테스트와 서비스 추상화
* 스프링 DI를 통해 테스트 대상의 의존 오브젝트를 변경하여 쉬운 테스트가 가능하다.
* 원활한 테스트만을 위해서도 서비스 추상화는 충분히 가치가 있다.

## 테스트 대역
* 테스트 대역: 테스트 환경을 만들어주기 위해 테스트 대상이 되는 오브젝트의 기능에만 충실하게 수행하면서 빠르게, 자주 테스트를 실행할 수 있도록 사용하는 오브젝트.
* 테스트 스텁: 테스트 대상 오브젝트의 의존 객체로서 존재하면서 테스트 동안에 코드가 정상적으로 수행할 수 있도록 돕는 것.
* 목 오브젝트: 테스트 오브젝트가 정상적으로 실행되도록 도와주면서, 테스트 오브젝트와 자신의 사이에서 일어나는 커뮤니케이션 내용을 저장해뒀다가 테스트 결과를 검증하도록 설계된 오브젝트.

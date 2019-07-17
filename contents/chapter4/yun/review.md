# 4장 예외

## 초난감 예외처리

* 모든 예외는 적절하게 복구되든지 아니면 작업을 중단시키고 운영자 또는 개발자에게 분명하게 통보돼야 한다.
* 긴 예외들을 처리하는 코드를 매번 thorws로 선언하기도 귀찮아져서 메소드 선언에 throws Exception을 기계적으로 붙이는 경우는 지양해야한다.

## 예외의 종류와 특징

#### Error
* java.lang.Error 클래스의 서브클래스들.
* 자바 VM에서 발생시키는 시스템 에러이므로 catch 블록으로 잡아봤자 아무런 대응 방법이 없다.

#### Exception과 체크 예외
* java.lang.Exception 클래스와 그 서브클래스들.
* 개발자들이 만든 애플리케이션 코드의 작업 중에 예외상황이 발생했을 경우에 사용.
* 체크 예외: Exception 클래스의 서브클래스이면서 RuntimeException 클래스를 상속하지 않은 것들.
* 언체크 예외: RuntimeException을 상속한 클래스들.
* RuntimeException은 Exception의 서브클래스이고 자바는 RuntimeException과 그 서브클래스를 특별하게 다룬다.
* 일반적으로 예외라고 하면 체크 예외라고 생각해도 된다.

#### RuntimeException과 언체크/런타임 예외
* java.lang.RuntimeException 클래스를 상속한 예외들.
* 명시적인 예외처리를 강제하지 않기 때문에 언체크 예외라고 불리거나 런타임 예외라고 불린다.
* 에러와 마찬가지로 catch 문으로 잡거나 throws를 선언하지 않아도 된다.
* 주로 프로그램의 오류가 있을 때 발생하도록 의도된 것들이다. ex) NullPointerException, IllegalArgumentException 등

#### 예외처리의 현실?
* 체크 예외가 예외처리를 강제하는 것 때문에 예외 블랙홀이나 무책임한 throws 같은 코드가 남발하며 비난의 대상이 되기도 했다.

#### 예외처리 방법
* 예외 복구: 예외상황을 파악하고 문제를 해결해서 정상 상태로 돌려놓는 방법.
* 예외처리 회피: 예외처리를 자신이 담당하지 않고 자신을 호출한 쪽으로 던져버리는 방법. ex) thorws 문으로 선언, catch 문으로 예외를 잡은 후 rethrow.
* 예외 전환: 예외 회피와 달리, 발생한 예외를 그대로 넘기는 게 아니라 적절한 예외로 전환해서 던지는 방법.
1. 내부에서 발생한 예외를 그대로 던지는 것이 그 예외상황에 대한 적절한 의미를 부여해주지 못하는 경우, 의미를 분명하게 해줄 수 있는 예외로 바꿔준다. (중첩 예외로 만드는 것이 좋다.)
2. 예외를 처리하기 쉽고 단순하게 만들기 위해 포장한다. 주로 예외처리를 강제하는 체크 예외를 언체크 예외인 런타임 예외로 바꾸는 경우에 사용한다.

#### 예외처리 전략
* 런타임 예외의 보편화: 자바의 환경이 서버로 이동하면서 체크 예외의 활용도와 가치는 점점 떨어지고 있고 대응이 불가능한 체크 예외라면 빨리 런타임 예외로 전환해서 던지는 게 낫다.
* 애플리케이션 예외: 시스템 또는 외부의 예외상황이 원인이 아니라 애플리케이션 자체의 로직에 의해 의도적으로 발생시키고, 반드시 catch 해서 무엇인가 조치를 취하도록 요구하는 예외를 일반적으로 애플리케이션 예외라고 한다.

#### DataAccessException
* 따로 정리하지 않음.

## 정리
* 예외를 잡아서 아무런 조취를 취하지 않거나 의미 없는 throws 선언을 남발하는 것은 위험하다.
* 예외는 복구하거나, 예외처리 오브젝트로 의도적으로 전달하거나, 적절한 예외로 전환해야한다.
* 좀 더 의미 있는 예외로 변경하거나, 불필요한 catch/throws를 피하기 위해 런타임 예외로 포장하는 두 가지 방법의 예외 전환이 있다.
* 복구할 수 없는 예외는 가능한 한 빨리 런타임 예외로 전환하는 것이 바람직하다.
* 애플리케이션의 로직을 담기 위한 예외는 체크 예외로 만든다.
* JDBC의 SQLException은 대부분 복구할 수 없는 예외이므로 런타임 예외로 포장해야 한다.
* SQLException의 에러 코드는 DB에 종속되기 때문에 DB에 독립적인 예외로 전환될 필요가 있다.
* 스프링은 DataAccessException을 통해 DB에 독립적으로 적용 가능한 추상화된 런타임 예외 계층을 제공한다.
* DAO를 데이터 엑세스 기술에서 독립시키려면 인터페이스 도입과 런타임 예외 전환, 기술에 독립적인 추상화된 예외로 전환이 필요하다.

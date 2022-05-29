# WIL #3
## 항해99 부트캠프 ing

### 객체 지향 프로그래밍 (Object-Oriented Programming, OOP)


 소프트웨어 엔지니어링에서 **의존성 주입**(dependency injection)은 하나의 객체가 다른 객체의 의존성을 제공하는 테크닉이다. "의존성"은 예를 들어 서비스로 사용할 수 있는 객체이다. 클라이언트가 어떤 서비스를 사용할 것인지 지정하는 대신, 클라이언트에게 무슨 서비스를 사용할 것인지를 말해주는 것이다. "주입"은 의존성(서비스)을 사용하려는 객체(클라이언트)로 전달하는 것을 의미한다. 서비스는 클라이언트 상태의 일부이다. 클라이언트가 서비스를 구축하거나 찾는 것을 허용하는 대신 클라이언트에게 서비스를 전달하는 것이 패턴의 기본 요건이다.

의존성 주입의 의도는 객체의 생성과 사용의 관심을 분리하는 것이다. 이는 가독성과 코드 재사용을 높혀준다.

의존성 주입은 광범위한 역제어 테크닉의 한 형태이다. 어떤 서비스를 호출하려는 클라이언트는 그 서비스가 어떻게 구성되었는지 알지 못해야 한다. 클라이언트는 대신 서비스 제공에 대한 책임을 외부 코드(주입자)로 위임한다. 클라이언트는 주입자 코드를 호출할 수 없다. 그 다음, 주입자는 이미 존재하거나 주입자에 의해 구성되었을 서비스를 클라이언트로 주입(전달)한다. 그리고 나서 클라이언트는 서비스를 사용한다. 이는 클라이언트가 주입자와 서비스 구성 방식 또는 사용중인 실제 서비스에 대해 알 필요가 없음을 의미한다. 클라이언트는 서비스의 사용 방식을 정의하고 있는 서비스의 고유한 인터페이스에 대해서만 알면 된다. 이것은 "구성"의 책임으로부터 "사용"의 책임을 구분한다.


* 의도

  의존성 주입은 다음과 같은 문제를 해결한다.

  - 어떻게 애플리케이션이나 클래스가 객체의 생성 방식과 독립적일 수 있는가?
  - 어떻게 객체의 생성 방식을 분리된 구성 파일에서 지정할 수 있는가?
  - 어떻게 애플리케이션이 다른 구성을 지원할 수 있는가?

  객체를 필요로하는 클래스 내에서 직접 객체를 생성하는것은 클래스를 특정 객체에 커밋하는 것이고 이후에 클래스로부터 독립적으로(클래스의 수정 없이) 인스턴스의 생성을 변경하는것이 불가능하기 때문에 유연하지 못하다. 이는 다른 객체를 필요로하는 경우 클래스를 재사용할 수 없게하며, 실제 객체를 모의 객체로 대체할 수 없기 때문에 클래스를 테스트하기 힘들게한다.

  클래스는 더 이상 객체 생성에 대한 책임이 없으며, 추상 팩토리 디자인 패턴에서처럼 팩토리 객체로 생성을 위임할 필요가 없다.

**개요**

  의존성 주입은 프로그램 디자인이 결합도를 느슨하게 되도록하고 의존관계 역전 원칙과 단일 책임 원칙을 따르도록 클라이언트의 생성에 대한 의존성을 클라이언트의 행위로부터 분리하는 것이다. 이는 클라이언트가 의존성을 찾기 위해 그들이 사용하는 시스템에 대해 알도록 하는 서비스 로케이터 패턴과 정반대되는 것이다.

  의존성 주입의 기본 단위인 주입은 새롭거나 관습적인 메커니즘이 아니다. "매개변수 전달"과 동일하게 동작한다. 주입으로써 "파라미터 전달"은 클라이언트를 세부 사항과 분리하기 위해 수행되고 있는 부가적인 의미를 전달한다.

  또한 주입은 전달을 제어하는 대상(클라이언트가 아님)에 대한 것이며 전달의 수행 방식-참조 또는 값 전달-과 독립적이다.

  의존성 주입은 네 가지 역할을 담당하는 객체 및 인터페이스를 전제로 한다.

  - 사용될 서비스 객체
  - 사용하는 서비스에 의존하는 클라이언트 객체
  - 클라이언트의 서비스 사용 방법을 정의하는 인터페이스
  - 서비스를 생성하고 클라이언트로 주입하는 책임을 갖는 주입자

  비유하자면,

  - 서비스 - 전기, 가스, 하이브리드 또는 디젤 자동차
  - 클라이언트 - 엔진에 상관 없이 동일하게 차를 사용하는 운전자
  - 인터페이스 - 운전자가 기어와 같은 엔진의 세부 사항을 이해할 필요가 없도록 보장해주는 자동변속기
  - 주입자 - 아이에게 어떤 차를 사줄지 결정하고 구매해준 부모

  사용될 수 있는 모든 객체는 서비스로 여겨진다. 다른 객체를 사용하는 모든 객체는 클라이언트로 여겨진다. 이름은 객체가 무엇을 위한 것인지와 무관하며 한 번의 주입에서 객체가 하는 역할과 관련이 있다.

  인터페이스는 클라이언트가 의존성으로 예상하는 타입이다. 쟁점은 무엇을 접근할 수 있게 하는가이다. 이는 실제로 서비스에 의해 구현된 인터페이스 타입일 수도 있지만 추상 클래스 또는 DIP를 위반하고, 테스트를 하기위한 동적으로 결합도 낮추는것을 희생하긴 하지만 concrete 서비스 자체일 수도 있다. 클라이언트가 인터페이스를 구성하거나 확장하는 것처럼 구체적으로 다룰 수 없도록 알지 못하게 하는 것이 요구된다.

  클라이언트는 의존성의 특정 구현에 대한 구체적인 지식이 필요 없다. 인터페이스의 이름과 API만 알면 된다. 결과적으로 인터페이스가 변경되더라도 클라이언트는 수정할 필요가 없어진다. 하지만 인터페이스가 클래스로 존재하다가 인터페이스 타입으로(그 반대의 경우에도) 리팩토링될 경우 클라이언트는 다시 컴파일이 필요할 수 있다. 이는 클라이언트와 서비스가 독립적으로 발행될 경우 중요하다. 이런경우에 결합도가 높아지는 문제는 안타깝게도 의존성 주입으로 해결할 수 없다.

  주입자는 클라이언트에게 서비스를 소개한다. 종종 클라이언트를 생성하기도 한다. 주입자는 객체를 클라이언트와 같이 처리하고 나중에 다른 클라이언트의 서비스로 처리하여 매우 복잡한 객체 그래프를 함께 연결할수도 있다. 주입자는 실제로 함께 동작하는 많은 객체가 될 수 있지만 클라이언트는 될 수 없다. 주입자는 다음과 같은 많은 이름들로 참조될 수 있다: assembler, provider, container, factory, builder, spring, construction code, or main.

  의존성 주입은 모든 객체가 구성과 동작을 분리하도록 요구하는 하나의 규율로 적용될 수 있다. 구성을 수행하는 DI 프레임워크에 의지하면 new 키워드의 사용을 금지하거나 덜 엄격하게 값 객체의 직접 생성을 허용할 수 있다.

* 장점

  소프트웨어 공학의 관점에서 볼 때 S/W의 질을 향상하기 위해 강한 응집력(Strong Cohesion)과 약한 결합력(Weak Coupling)을 지향해야 하는데, OOP의 경우 하나의 문제 해결을 위한 데이터를 클래스에 모아 놓은 데이터형을 사용함으로써 응집력을 강화하고, 클래스간에 독립적인 디자인을 함으로써 결합력을 약하게 한다.


* 장점

  - 의존성 주입은 클라이언트의 구성 가능성을 유연하게 해준다. 클라이언트의 행위는 고정되어 있다. 클라이언트는 클라이언트가 기대하는 고유한 인터페이스를 지원하는 모든 것을 할 수 있다.

  - 의존성 주입을 통해 시스템의 구성 세부 사항을 외부의 구성 파일에서 사용하여 리컴파일 없이 시스템을 재 구성할 수 있다. 분리된 구성은 컴포넌트의 여러 구현을 요구하는 다양한 상황을 위해 작성될 수 있다. 이는 국한되어 있지는 않지만 테스팅을 포함한다.

  - 의존성 주입은 코드의 동작에서의 어떠한 변경도 요구하지 않으므로리팩터링으로써 레거시 코드에도 적용할 수 있다. 클라이언트는 더 독립적이며 테스트에 속하지 않은 다른 객체를 가장하는 stubs 또는 모의 객체를 사용해 독립된 유닛 테스가 더 쉬워지는 결과를 얻는다.

  - 의존성 주입을 통해 클라이언트는 사용해야하는 모든 구체적인 구현에 대한 지식을 제거할 수 있다. 디자인 변경이나 결함의 영향으로부터 클라이언트를 독립하는데 도움을 주며, 이는 재사용성, 테스트가능성, 유지가능성을 향상시킨다.


출처 : 위키피디아 [https://ko.wikipedia.org/wiki/%EC%9D%98%EC%A1%B4%EC%84%B1_%EC%A3%BC%EC%9E%85](https://ko.wikipedia.org/wiki/%EC%9D%98%EC%A1%B4%EC%84%B1_%EC%A3%BC%EC%9E%85)




### 제어 반전


* 자바 가상 머신이란?

  제어 반전, 제어의 반전, 역제어는 프로그래머가 작성한 프로그램이 재사용 라이브러리의 흐름 제어를 받게 되는 소프트웨어 디자인 패턴을 말한다. 줄여서 IoC(Inversion of Control)이라고 부른다. 전통적인 프로그래밍에서 흐름은 프로그래머가 작성한 프로그램이 외부 라이브러리의 코드를 호출해 이용한다. 하지만 제어 반전이 적용된 구조에서는 외부 라이브러리의 코드가 프로그래머가 작성한 코드를 호출한다. 설계 목적상 제어 반전의 목적은 다음과 같다:

  * 작업을 구현하는 방식과 작업 수행 자체를 분리한다.
  * 모듈을 제작할 때, 모듈과 외부 프로그램의 결합에 대해 고민할 필요 없이 모듈의 목적에 집중할 수 있다.
  * 다른 시스템이 어떻게 동작할지에 대해 고민할 필요 없이, 미리 정해진 협약대로만 동작하게 하면 된다.
  * 모듈을 바꾸어도 다른 시스템에 부작용을 일으키지 않는다.


* 예

  ```java
  public class ServerFacade
  {
    public Object respondToRequest(Object pRequest)
    {
      if(businessLayer.validateRequest(pRequest))
      {
        DAO.getData(pRequest);
        return Aspect.convertData(pRequest);
      }

      return null;
    }
  }
  ```

  위의 코드를 통해 IoC가 어떻게 이용되는지를 알 수 있다. 위에서 serverFacade에서 DAO 객체를 이용할 때 businessLayer객체가 pRequest를 검증하는 방법과 Aspect 객체가 DAO에서 처리한 pRequest를 변환하는 방법이 미리 정해져 있다. 이와 같이 정해진 방법들이 유효할 때도 있겠지만, 이 방법들을 정해 두면 serverFacade 클래스는 DAO와 결합되게 된다. 제어 반전 개념으로 다음과 같이 응용 프로그램을 설계하면 제어권을 완전히 DAO 객체로 이양하게 된다.

  ```java
  public class ServerFacade
  {
    public Object respondToRequest(Object pRequest, DAO dao)
    {
      return dao.getData(pRequest);
    }
  }
  ```

  이 예를 보면, respondToRequest라는 메서드가 인자들을 다루는 방식을 통해 IoC가 적용되었는지 여부를 확인할 수 있다.

출처 : 위키피디아 [https://ko.wikipedia.org/wiki/%EC%A0%9C%EC%96%B4_%EB%B0%98%EC%A0%84](https://ko.wikipedia.org/wiki/%EC%A0%9C%EC%96%B4_%EB%B0%98%EC%A0%84)




### 스프링 빈(Spring Bean)

  Spring IoC 컨테이너가 관리하는 자바 객체를 빈(Bean)이라고 부른다.

  보통의 Java Programming 에서는 Class를 생성하고 new를 입력하여 원하는 객체를 직접 생성한 후에 사용하지만, Spring에서는 직접 new를 이용하여 생성한 객체가 아니라, Spring에 의하여 관리당하는 자바 객체를 사용한다. 이렇게 Spring에 의하여 생성되고 관리되는 자바 객체를 Bean이라고 한다. Spring Framework 에서는 Spring Bean 을 얻기 위하여 ApplicationContext.getBean() 와 같은 메소드를 사용하여 Spring 에서 직접 자바 객체를 얻어서 사용한다.



**Spring Bean을 Spring IoC Container에 등록하는 방법**


  1. 자바 어노테이션(Java Annotation)을 사용하는 방법

      JAVA에서 Annotation은 자바 소스 코드에 추가하여 사용할 수 있는 메타데이터의 일종이다.
      Java에서는 @Override, @Deprecated 와 같은 기본적인 Annotation을 제공한다.

      Spring에서는 여러 가지 Annotation을 사용하지만, Bean을 등록하기 위해서는 @Component Annotation을 사용한다. @Component Annotation이 등록되어 있는 경우에는 Spring이 Annotation을 확인하고 자체적으로 Bean 으로 등록한다.

      실제 Spring 프로젝트에서 Controller를 등록할 때에는 아래와 같은 Annotation을 사용한다. 아래의 예시에서 Controller 임을 Spring 에게 알려주기 위하여 @Controller Annotation을 사용했다.

      ```java
      // HelloController.java
      @Controller
      public class HelloController {
          // @GetMapping Annotation을 사용하여 Mapping을 사용
          @GetMapping("hello")
          public String hello(Model model){
              model.addAttribute("data", "This is data!!");
              return "hello";
          }
      }
      ```

      @Controller Annotation을 intelliJ에서 Ctrl 을 눌러서 이동해보면 아래와 같은 소스를 확인할 수 있다. @Controller Annotation에는 @Component Annotation이 있는 것을 확인할 수 있다. @Component Annotation 으로 인하여 Spring은 해당 Controller를 Bean 으로 등록한다.

      ```java
      // Controller.java

      // -- 일부 생략 --
      @Target({ElementType.TYPE})
      @Retention(RetentionPolicy.RUNTIME)
      @Documented
      @Component
      public @interface Controller {
        /**
        * The value may indicate a suggestion for a logical component name,
        * to be turned into a Spring bean in case of an autodetected component.
        * @return the suggested component name, if any (or empty String otherwise)
        */
        @AliasFor(annotation = Component.class)
        String value() default "";
      }
      ```
  

  2. Bean Configuration File에 직접 Bean 등록하는 방법

      @Configuration과 @Bean Annotation 을 이용하여 Bean을 등록할 수 있다. 아래의 예제와 같이 @Configuration을 이용하면 Spring Project 에서의 Configuration 역할을 하는 Class를 지정할 수 있다. 해당 File 하위에 Bean 으로 등록하고자 하는 Class에 @Bean Annotation을 사용해주면 간단하게 Bean을 등록할 수 있다.

      ```java
      // Hello.java
      @Configuration
      public class HelloConfiguration {
          @Bean
          public HelloController sampleController() {
              return new SampleController;
          }
      }
      ```




출처 : [https://melonicedlatte.com/2021/07/11/232800.html](https://melonicedlatte.com/2021/07/11/232800.html)


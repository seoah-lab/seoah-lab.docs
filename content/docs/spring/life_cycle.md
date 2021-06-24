# Spring Bean Lifecycle

Lifecycle을 이용해서

Spring 은 IoC 를 통하여 Bean을 관리하는 프레임 워크이다.

Bean 컨테이너(ApplicationContext)의 핵심 기능은 애플리케이션에 필요한 Bean(DI 작업이 완료되어 실행 가능한 상태의 Bean)을 생성하고, 초기화하는 것이다.

ApplicationContext는 Bean 생성 및 관리에 대한 책임을 BeanFactory에게 모두 위임한다. 즉, Spring Framework에서 Bean Lifecycle 관리에 대한 모든 책임은 BeanFactory가 가진다.


Bean의 라이프 사이클은 다음과 같은 단계로 진행된다.
생성(Create)
초기화(Init)
사용(Service)
소멸(Destory) 

Bean 생성
Bean의 생성은 IoC Container를 통해 진행(싱글톤 방식)
싱글톤 방식 -> 인스턴스가 없다 : 생성 / 있다 : 사용 방식으로 처리

Bean 초기화
Bean 생성 이후 초기화를 수행
초기화를 하기 위한 다양한 방법을 제공하고 있음 (토비 스프링 3.1  186P 참고)
InitialIzingBean 구현
init-method지정 (xml or java  annotation config)
@PostConstruct 지정

Bean 사용
IoC Container를 통해 생성된 Bean을 마음껏 사용
반복적으로 사용되더라도 인스턴스가 신규로 생성되지 않는 한 초기화는 발생하지 않는다.

Bean 소멸
컨테이너가 종료될 때 destory 메소드가 선언되어 있다면 수행
소멸 시 사용할 수 있는 다양한 destroy 방법이 있음
DisponsableBean 인터페이스를 직접 구현 (destroy() 메소드)
destroy-method를 넣어서 destory 시점에 동작 수행 (xml or java annotation config)
@Predestory 지정

---

참고 자료

https://www.slipp.net/wiki/pages/viewpage.action?pageId=25528047
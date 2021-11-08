## 스프링 부트

![image-20211101101644207](img/image-20211101101644207.png)



- 스프링 프레임워크 기반 프로젝트를 복잡한 설정없이 쉽고 빠르게 만들어주는 라이브러리

- 사용자가 일일이 모든 설정을 하지 않아도 자주 사용되는 **기본설정을 해줌**

  (스프링 프레임워크에서는 XML설정파일(web.xml, applicationContext.xml, ServletContext.xml 등)들을 작성해야 헀다.)



### 특징

**1) 라이브러리 관리 자동화**

스프링 부트의 **Starter** 라이브러리를 등록해서 라이브러리의 의존성을 간단하게 관리할 수 있다.



**2)설정의 자동화**

스프링 부트에서는 프로젝트에 추가된 라이브러리를 기반으로 실행에 필요한 환경을 자동으로 설정해준다.



**3)라이브러리 버전 자동 관리**

기존에는 스프링 라이브러리의 버전을 하나하나 직접 입력해야 했지만, 스프링 부트는 pom.xml에 스프링 부트 버전을 입력하면 스프링 라이브러리 뿐만 아니라 서드 파티 라이브러리들도 호환되는 버전으로 알아서 설정해준다.



**4)내장 Tomcat**

스프링 부트는 Tomcat을 내장하고 있기 때문에 @SpringBootApplication어노테이션이 선언되어있는 클래스의 main() 메소드를 실행하는 것만으로 서버를 구동시킬수 있다.



**5)독립적으로 실행 가능한 JAR**

웹 프로젝트라면 WAR 파일로 패키징해야하지만 스프링 부트는 내장 톰캣을 지원하기 때문에 JAR 파일로 패키징해서 웹 애플리케이션을 실행시킬 수 있다.



### meta-annotaiton ?

**`meta-annotation`** 은 다른 annation 에서도 사용되는 annotation 의 경우를 말하며 **`custom-annotation`** 을 생성할 때 주로 사용된다.

예를 들어, **`@Service`** 은 bean 으로 등록해주기 위해 **`@Component`** 을 내포하고 있는 형태로, 여기서 **`@Component`** 가 meta-annotation 이다.

```
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component // Spring will see this and treat @Service in the same way as @Component
public @interface Service {

// ....
}
    
```

이런 meta-annotaion 중 **`@Target`** 과 **`@Retention`** 에 대해서 알아보자.

 

### @Target

**`@Target`** 은 Java compiler 가 annotation 이 어디에 적용될지 결정하기 위해 사용다.

예를 들어 위에서 사용한 @Service 의 **`ElementType.TYPE`** 은 해당 Annotation 은 **`타입 선언`** 시 사용한다는 의미다.

종류는 다음과 같다.

```
ElementType.PACKAGE : 패키지 선언
ElementType.TYPE : 타입 선언
ElementType.ANNOTATION_TYPE : 어노테이션 타입 선언
ElementType.CONSTRUCTOR : 생성자 선언
ElementType.FIELD : 멤버 변수 선언
ElementType.LOCAL_VARIABLE : 지역 변수 선언
ElementType.METHOD : 메서드 선언
ElementType.PARAMETER : 전달인자 선언
ElementType.TYPE_PARAMETER : 전달인자 타입 선언
ElementType.TYPE_USE : 타입 선언
    
```



### @Retention

**`@Retetion`** 은 Annotation 이 실제로 적용되고 유지되는 범위를 의미한다.

Policy 에 관련된 Annotation 으로 컴파일 이후에도 JVM 에서 참조가 가능한 RUNTIME 으로 지정한다.

종류는 다음과 같다.

```
RetentionPolicy.RUNTIME
RetentionPolicy.CLASS
RetentionPolicy.SOURCE
    
```

**`RetentionPolicy.RUNTIME`** 은 컴파일 이후에도 JVM 에 의해서 계속 참조가 가능하다. 주로 리플렉션이나 로깅에 많이 사용된다.

**`RetentionPolicy.CLASS`** 은 컴파일러가 클래스를 참조할 때가지 유효하다.

**`RetentionPolicy.SOURCE`** 은 컴파일 전까지만 유효하다. 즉, 컴파일 이후에는 사라지게 된다.

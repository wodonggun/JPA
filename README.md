# JPA


## JPA
이번 글에서는 JPA(Java Persistence API)가 무엇인지 알아보려고한다. JPA는 자바 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용되는 인터페이스의 모음이다. 그 말은 즉, 실제적으로 구현된것이 아니라 구현된 클래스와 매핑을 해주기 위해 사용되는 프레임워크이다. JPA를 구현한 대표적인 오픈소스로는 Hibernate가 있다.

ORM(Object-Relational Mapping) 우리가 일반 적으로 알고 있는 애플리케이션 Class와 RDB(Relational DataBase)의 테이블을 매핑(연결)한다는 뜻이며, 기술적으로는 어플리케이션의 객체를 RDB 테이블에 자동으로 영속화 해주는 것이라고 보면된다.

JPA(Java Persistence API) Java 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용하는 인터페이스 모음 자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스 인터페이스 이기 때문에 Hibernate, OpenJPA 등이 JPA를 구현함

![image](https://user-images.githubusercontent.com/35188271/174612482-930a3cf9-a01c-4b93-a5f0-1c5dde793ca0.png)
![image](https://user-images.githubusercontent.com/35188271/174612507-5adffcbc-c983-4049-8ca2-81593e0bc24e.png)



## intro
JPA는 단순하게 쿼리를 짜지않고, 코드도 적어서 개발 속도가 빨라짐.  
- 예시  
![image](https://user-images.githubusercontent.com/35188271/162733055-760b4342-7356-4935-9408-63b7cc7f32de.png)  


## JPA 공부 목표
![image](https://user-images.githubusercontent.com/35188271/162733384-2011f044-240d-4890-abb8-872a40dbb823.png)  

![image](https://user-images.githubusercontent.com/35188271/162733690-e2086267-a3d0-4bc7-b459-d8bee9fce380.png)  


## ORM
`ORM(Object-relation mapping)` : 객체 관계 매핑 프레임워크  
`JPA(Java persistence API` : 자바 ORM 표준  

- JPA 구조  
![image](https://user-images.githubusercontent.com/35188271/162744206-8e5dca73-37f3-4a4b-b21b-e961862748c5.png)  

![image](https://user-images.githubusercontent.com/35188271/162744483-c5c85ade-9fbb-42a5-8ffa-50999f470470.png)  

## 지연 로딩 / 즉시 로딩

지연 로딩 : 객체가 실제 사용될 때 로딩  
![image](https://user-images.githubusercontent.com/35188271/162746103-325ab37d-8e79-480c-bf9c-a887a200a854.png)  
부모객체 member를 가져오고, getTeam()을 통해 자식객체(껍데기)를 가져왔는데, team.getName()을 호출하면 직접 db에 쿼리를 날려서 자식객체(Team)에 대한 정보를 가져옴.  

즉시 로딩 : JOIN SQL로 한번에 연관된 객체까지 미리 가져옴.  
![image](https://user-images.githubusercontent.com/35188271/162747193-77effd4b-2fc7-44a3-a4bb-0314b0edeb4e.png)  

: 대부분 지연 로딩으로 기본적으로 사용하고, 최적화가 필요할때 직접 필요한곳에 JPA옵션 세팅을 통해서 즉시로딩으로 변경함.  



## SQL JPQL JPA
SQL은 데이터베이스 테이블을 대상으로 조인해서 가져옴.
JPQL은 엔티티 객체를 대상으로 쿼리로 가져옴.
![image](https://user-images.githubusercontent.com/35188271/162771815-8133eb68-3a1a-4916-a2ea-b5e780eca38a.png)  
Member객체를 테이블로써 가져옴.
    

 

## 엔티티 vs 값타입
- 기본값 타입 : int,double,Long, String 등 기본 타입들
- 임베디드 타입 : 값을 묶어서 하나의 객체느낌으로 컬럼을 쓰고싶을때
- 컬렉션 값 타입 : 

```
기본값 타입은 절대 대입식으로 쓰면 안됨. 자바는 주소 참조방식이기 때문에
int a = 10;
int b = 0;
b = a; 를 선언하면 서로 객체가 참조되어 개발자의 의도는 b에 새로운값을 넣으려고했던건데 추후에 수정으로 a에도 변경이 생겨 사이드 이펙트가 일어날 수 있음.
```


## 임베디드 타입

```
주소 Address객체를 임베디드해서 사용하는데, Hone주소와 Work주소를 둘다 가지고 싶으면?

@AttributeOverrides, @AttributeOverride를 사용해서
컬러 명 속성을 재정의
```

단점 : 임베디드 타입은 여러 엔티티에서 공유해서 사용하면 문제가 생김.
그래서 여러 엔티티에서 공유하려고하면 차라리 엔티티로 만들어야함.

  
`값 객체를 왜 VO를 생성하고, 파괴만 가능하고, 수정은 불가능하게 가이드 했는지?`  
```
member.getHomeAddress().setCity("수원시")로 update를 날려도
member2 엔티티(row)에도 update가 날아감...버그?

(JPA강의 - 값 타입과 불변 객체 - 6:00)
```
![image](https://user-images.githubusercontent.com/35188271/173843919-11e5c802-ef19-4929-b0f1-ac9b59aaddc7.png)  
불변 객체를 통해서 부작용을 원천 차단 가능함.
불변객체는 Setter를 사용하지않고, 생성자에서 다 설정하고 수정 불가능해야함.



## 

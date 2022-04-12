# JPA

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
    

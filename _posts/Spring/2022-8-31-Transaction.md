---
title:  "[Development] Transaction (@Transactional / JPA)"
date: 2022-9-2 3:00PM
excerpt: "Dev"

author: Yuha
categories: [Development, Spring]
tags: [eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-9-2 1:00PM
---

# Spring @Transactional
- Option
  - Isolation Level
  - Propagation
  - no-rollback for
- Step transaction in Tasklet (job) of Spring batch

# Spring JPA
- Persistence Context
  - @OneToMany, @ManyToMany, @ManyToOne, @OneToOne Option
    - FetchType
    - CascadeType
    - orphanRemoval
  - @Embeddable, @Embedded
  - LockModeType

---

# Spring @Transactional

---

## Isolation Level

- Default

- `READ_UNCOMMITTED`
: can read uncommited datas.
  - allows dirty read (it can occur bad data consistency)
  - prevents nothing.
  - READ_UNCOMMITTED setting is <b>the fastest.</b>

- `READ_COMMITTED` (often used)
: can read committed datas.
  - allows non-repeatable read
  - prevents just one, Dirty reads

- `REPEATABLE_READ`
  - allows phantom read (= repeatable read)
  - prevents two anomalies: Dirty reads, Non-repeatable reads

- `SERIALIZABLE`
  - prevents all three anomalies: Dirty reads, Non-repeatable reads and Phantom reads
  - makes transactions <b>very slow</b>

- (weak) Read Uncommited < Read Committed < Repeatable Read < Serializable (strong)

- if you want to use more high isolation level, use LockModeType

<img width="714" alt="Screen Shot 2022-09-01 at 3 36 31 PM" src="https://user-images.githubusercontent.com/83699657/187847870-9f6ad19e-99ef-4390-9319-da608092b8c1.png">

![isolation level](https://user-images.githubusercontent.com/83699657/187634937-97efc86c-42b0-4d72-b90c-8f465a618e74.png)

---

## Dirty Read VS Phantom Read VS Non-repeatable Read

|**Dirty Read**|**Phantom Read (= repeatable read)**|**Non-repeatable Read**|
|:---:|:---:|:---:|
|read **UNCOMMITED data** from another transaction.|read **COMMITTED data from an UPDATE query** from another transaction.|read **COMMITTED data from an INSERT or DELETE query** from another transaction.|

`Dirty Checking`
- JPA에서는 Entity를 조회하면 해당 Entity의 조회 상태 그대로를 Snapshot을 만들어 놓음
- 트랜잭션이 끝나는 시점에 해당 Snapshot과 비교해 다른 점이 있다면 Update Query를 DB에 전달함

reference : <https://jojoldu.tistory.com/415>


---

## Propagation

```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
@Transactional(propagation = Propagation.NEVER)
```

```
if any component or service will or will not participate in transaction 
and how will it behave if the calling component/service already has or does not have a transaction created already.
```

- REQUIRED (default)
: Support a current transaction; create a new one if none exists.
  -  부모 트랜잭션 내에서 실행하며 부모 트랜잭션이 없을 경우 새로운 트랜잭션을 생성

- SUPPORTS
: Support a current transaction; execute non-transactionally if none exists.
  - 부모 트랜잭션 내에서 실행하며 부모 트랜잭션이 없을 경우 nontransactionally로 실행

- MANDATORY
: Support a current transaction; throw an exception if no current transaction exists. 
  - 부모 트랜잭션 내에서 실행되며 부모 트랜잭션이 없을 경우 예외가 발생

- REQUIRES_NEW
: Create a new transaction, suspending the current transaction if one exists. 
  - 부모 트랜잭션을 무시하고 무조건 새로운 트랜잭션이 생성

- NOT_SUPPORTED
: Do not support a current transaction; rather always execute non-transactionally.
  - nontransactionally로 실행하며 부모 트랜잭션 내에서 실행될 경우 일시 정지

- NEVER
: Do not support a current transaction; throw an exception if a current transaction exists.
  - nontransactionally로 실행되며 부모 트랜잭션이 존재한다면 예외가 발생

- NESTED
: Execute within a nested transaction if a current transaction exists, behave like PROPAGATION_REQUIRED otherwise.
  - 둘러싼 트랜잭션이 없을 경우 REQUIRED와 동일하게 작동. 해당 메서드가 부모 트랜잭션에서 진행될 경우 별개로 커밋되거나 롤백될 수 있음.


reference : <https://jsonobject.tistory.com/467>

---

## no-rollback for

```java
@Transactional(noRollbackFor = RuntimeException.class)
```


- 특정 예외가 발생하더라도 롤백되지 않도록 설정


---

## Read only

```
@Transactional(readOnly = true)
```

- Entity를 read only로 조회하면, 변경 감지를 위한 snapshot을 유지하지 않아도 되고, 영속성 컨텍스트를 flush하지 않아도 되 성능을 향상 시킬 수 있음.

- other way : scala type in query
```
select o.id, o.name from Order o
```


---
# Spring JPA

---

## Persistence Context

```
the first-level cache where all the entities are fetched from the database or saved to the database.
```

- Persistence context <b>keeps track of any changes</b> made into a managed entity.
- If anything changes during a transaction, then the entity is marked as <b>dirty</b>. When the transaction completes, these changes are <b>flushed</b> into persistent storage.
- <b>An EntityManager</b> is associated with a persistence context.
- It sits <b>between our application and persistent storage.</b>

- PersistenceContextType
  - Transaction-scoped persistence context (default)
  - If one exists, then it will be used. Otherwise, it will create a persistence context.
  ```java
  @PersistenceContext
  private EntityManager em;
  ```

  - Extended-scoped persistence context
  - it can span across multiple transactions. We can persist the entity without the transaction but cannot flush it without a transaction.
  
  ```java
  @PersistenceContext(type = PersistenceContextType.EXTENDED)
  ```
<img width="1087" alt="Screen Shot 2022-09-01 at 2 16 51 PM" src="https://user-images.githubusercontent.com/83699657/187836817-1306e0c8-4943-4942-aab9-7ce45c4aa976.png">
<img width="1071" alt="Screen Shot 2022-09-01 at 2 16 45 PM" src="https://user-images.githubusercontent.com/83699657/187836802-78521c2c-0790-4027-9bd9-0d566f3d8842.png">

reference : <https://www.baeldung.com/jpa-hibernate-persistence-context>


---

## EntityManager

```java

@PersistenceContext
private EntityManager em;

Member member = em.find(Member.class, "member1"); // get entity
transaction.commit();
em.close(); // End persistence context

```

---

## @OneToMany, @ManyToMany, @ManyToOne, @OneToOne Option

- `FetchType`
: see next part

- `CASCADE`
: to inherit persistence
  - CascadeType
    - ALL, PERSIST, MERGE, REMOVE, REFRESH, DETACH

- `orphanRemoval`
: to remove child entity together when the parent entity is not related anymore
  - orpahnRemoval = true
    : remove the related child entity automatically

`example`
```java
// can add or remove child entity when the parent entity is added or removed
@OneToMany(mappedBy = "parentClassName", cascade = {CascadeType.ALL}, orphanRemoval = true)
private List<> ... = ...;


Parent parent = em.find(Parent.class, parentld);

// CascadeType.ALL =
parent.addChild(child); 

// orphanRemoval = true =
parent.getChildren().remove(object); 
```

---

## FetchType 

- `Lazy Loading` (Recommend)
: delays the initialization of a resource. (get proxy)
  - the default of @OneToMany, @ManyToMany
    - (optional = false) : inner join
    - (optional = true) : outer join

`example`
```java
@ManyToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "TEAM_ID", nullable = false)
private Team team;

Member member = em.find(Member.class, "member1");
Team team = member.getTeam(); // proxy object
team.getName(); // use real object (search data from DB on this time)

// proxy
Member member = em.getReference(Member.class, "member1");
```
  - find() : If there is no entity in the persistence context, search data from database.


- `Eager Loading`
: initializes or loads a resource as soon as the code is executed. (get data immediately)
  - often use it with **JOIN query**
  - the default of @ManyToOne, @OneToOne
    - (optional = false) : outer join
    - (optional = true) : inner join

`example`
```java
@ManyToOne(fetch = FetchType.EAGER)
@JoinColumn(name = "TEAM_ID", nullable = false)
private Team team;

Member member = em.find(Member.class, "member1");
Team team = member.getTeam(); // get real object
```  
---

## @Embeddable, @Embedded

- `@Embeddable`
: use on the defined value

- `@Embedded`
: use on the being used value

`example`
```java
@Entity
public class Member {
  String name;

  @Embedded
  Address address;
}

@Embeddable
public class Address {
  String city;
  String street;
}
```

- you can use `@AttributeOverride` if there are duplicated properties.

---

## LockModeType
`control DB concurrency`

- READ (= OPTIMISTIC)

- WRITE (= OPTIMISTIC_FORCE_INCREMENT)

- OPTIMISTIC (= READ)

- OPTIMISTIC_FORCE_INCREMENT (= WRITE)

- PESSIMISTIC_READ

- PESSIMISTIC_WRITE

- PESSIMISTIC_FORCE_INCREMENT

- NONE

`Optimistic`
- assume transaction will <b>not</b> be occured
- how to apply : Use `@Version` in JPA

- Entity 내부에 @Version이 붙은 int, Integer, long, Long, short, Short, Timestamp Type의 필드가 있으면 적용됨 (한 개의 필드만 허용)

- **OPTIMISTIC**
  - 읽기 시에도 ＠Version 속성을 체크하고 트랜잭션이 종료될 때까지 다른 트랜잭션에서 변경하지 않음을 보장 (Dirty Read 방지)

- **OPTIMISTIC_FORCE_INCREMENT**
    - @Version 정보를 강제로 증가시킴

`Pessimistic`
- assume transaction will be occured
- transaction will wait before getting Lock
- how to apply : Use Lock on DB

- **PESSIMISTIC_WRITE** (often used in PESSIMISTIC LOCK)
  - select for update
  - lock이 걸린 row는 다른 transaction이 read, update, delete 할 수 없음 (prevent non-repeatable read)

- **PESSIMISTIC_READ**
  - only read / update, delete되는 것을 방지 / for share

- **PESSIMISTIC_FORCE_INCREMENT**
  - Use @Version / 잠금을 획득할 시 @Version이 업데이트됨 / for update nowait

### Recommend JPA Transaction
- Read committed transaction + Optimistic Version management

reference : <https://velog.io/@lsb156/JPA-Optimistic-Lock-Pessimistic-Lock>

---

## Primary Cache, Secondary Cache
- primary cache
: in persistence context

- secondary cache
: in application before terminating application

- `@Cacheable(cacheNames = "")`
: enable caching
  - first check the cache before actually invoking the method and then caching the result.
  - must have the return value

- `@CacheEvict(cacheNames = {..., ...})`
: to indicate the removal of one or more/all values so that fresh values can be loaded into the cache again.
  - the return value is not needed
  - `@CacheEvict(value="...", allEntries=true)`
  : this will **clear all the entries in the caches** and prepare it for new data.

- `@CachePut`
: we can update the content of the cache without interfering with the method execution. That is, the method will always be executed and the result cached:
  - `@CachePut` will actually run the method and then put its results in the cache, whereas `@Cacheable` will skip running the method and first check the cache.

- `@Caching`
  - @Caching(evict = {...}), group multiple caching annotations

- `@CacheConfig`
: we can streamline some of the cache configuration into a single place at the class level, so that we don't have to declare things multiple times

- `AopContext.currentProxy()`
  - to use this proxy, declare `@EnableAspectJAutoProxy(exposeProxy = true)` in configuration
  - `@EnableCaching` in CachingConfig
    - After we enable caching, for the minimal setup, we must register a `cacheManager`
  - `@Aspect`


```java
// @Cacheable
@Cacheable(cacheNames = "member")
public List<MemberDto> getMembers() {
  return api.getMembers();
}

// AopContext.currentProxy()
public List<MemberDto> getMembersOver30age() {
  return AopContext.currentProxy().getMembers()
    .stream().filter(age -> age > 30)
    .collect(Collectors.toList());
}
```

```java
// Api
@CacheEvict(cacheNames = MEMBER)
@PostMapping
String registerMember(Member member);

@CacheEvict(cacheNames = MEMBER)
@PutMapping
void modifyMember(String memberCode, Member member);
```

reference : <https://www.baeldung.com/spring-cache-tutorial>

---

## EntityTransaction

- public void begin();

- public void commit();

- public void rollback();

- public void setRollbackOnly();

- public boolean getRollbackOnly();

- public boolean isActive();

---

# Word
- Data Consistency : 데이터 정합성 (데이터 값이 서로 일치하는 상태)
- Data Integrity : 데이터 무결성 (데이터 값이 정확한 상태)
---
layout: post
title: "postgreSQL 이란 ?"
date: 2022-05-04 08:00:00 +0530
categories: DB, SQL, noSQL, RDBMS
comments_id: 2
---

postgreSQL과 mySQL의 차이와 더불어 SQL과 noSQL의 차이를 다루었습니다.

<br>

> 파이어베이스를 활용한 프로토타입 개발이 끝나고 version-1을 준비함에 있어서 DB를 먼저 정하자는 회의가 있었다. 우리가 postgreSQL을 선택한 경위에 대해 설명하려고 한다.

## DB

<hr>

여러 사람이 공유하고 사용할 목적으로 통합 관리되는 정보의 집합.

**논리적으로 연관된 하나 이상의 자료 모음으로 그 내용을 고도로 구조화하여 검색 및 갱신의 효율을 높임**

- 자료의 중복을 없앤다
- 자료끼리의 관련성을 갖게 한다
- 어떤 방식으로 자료끼리 관련성을 갖게 할까?

**DB 특징**

- 실시간 접근성
- 계속적인 진화(업데이트가 쉽다)
- 동시 공유(같이 쓸 수 있는것)
- 내용에 의한 참조(데이터 베이스에서는 데이터의 주소나 위치로 찾지 않는다.)
- 데이터 논리적 독립성

_DB 장점_

_데이터 중복 최소화_

_데이터 공유_

_일관성, 무결성, 보안성 유지_

_최신의 데이터 유지_

_데이터의 표준화 가능_

_데이터의 논리적, 물리적 독립성_

_용이한 데이터 접근_

_데이터 저장 공간 절약_

<br>

**데이터 베이스를 조작하는 별도의 소프트웨어**

무결성, 일관성, 유용성을 보장하기 위해서 자료를 제거하고 관리하는 소프트웨어 체계

응용 프로그램들이 데이터베이스에 접근할 수 있는 인터페이스를 제공

데이터베이스 기술의 추세를 살펴보면, 종전의 파일형 데이터베이스에서 관계형 데이터베이스(RDBMS)를 거쳐 최근에는 오브젝트 지향 데이터베이스(가 주류를 형성

`관계형 데이터베이스 관리 시스템`(RDBMS)

- mySQL, ORACLE, msSQL

`인 메모리 데이터베이스 관리 시스템`(IMDBMS)

`기둥형 데이터베이스 관리 시스템`(CDBMS)

<br>

## SQL(관계형 DB)

<hr>

### SQL(관계형 DB)

관계형 DBMS에서 데이터를 조회, 수정, 삭제하거나, DBMS를 조작하는데 사용되는 언어인 SQL(Structured Query Language)

DBMS`Database Management Systems`에서 데이터를 저장, 수정, 삭제 및 검색

**특징**

- 데이터는 정해진 데이터 스키마에 따라 테이블에 저장된다.
- 데이터는 관계를 통해 여러 테이블에 분산된다

테이블에 레코드로 저장되는데, 각 테이블마다 명확하게 정의된 구조가 있다. 해당 구조는 필드의 이름과 데이터 유형으로 정의된다.

고로, 스키마를 준수하지 않은 레코드는 테이블에 추가할 수 없다

![994D09355C937ECD2D.jpeg](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bb839893-19e4-4224-8433-4630141eaf39/994D09355C937ECD2D.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220530%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220530T110616Z&X-Amz-Expires=86400&X-Amz-Signature=ad4e513976766eb9b383b3ccfbabcbfb15fcbd7ed7fbaa49337b68c27bf59649&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22994D09355C937ECD2D.jpeg%22&x-id=GetObject)

<br>

**확장**

수직적 확장만 지원 : 단순히 데이터베이스 서버의 성능을 향상시키는 것 (ex. CPU 업그레이드)

<br>

<br>

## NoSQL (비관계형 DB)

<hr>

mongoDB, firebase 생각하면 되겠다.

스키마도 없고, 관계도 없다.

레코드는 Json과 비슷한 형태로 가지고 있다. 문서(documents)라고 부른다.

NoSQL에서는 다른 구조의 데이터를 같은 컬렉션에 추가가 가능하다.

필요한 모든 것을 갖춘 문서를 작성하는 것이 NoSQL이다.

- `필요한 모든 것?`

  문서는 Json과 비슷한 형태로 가지고 있으나 관계형 데이터 베이스처럼 여러 테이블에 나누어 담지 않고, 관련 데이터를 동일한 '컬렉션'에 넣습니다. \
   위 사진의 Orders, Users, Products 테이블로 나누는 작업이 필요없습니다. \
   테이블을 합치는 `조인`이라는 개념이 존재하지 않습니다. JOIN

  - 조인이 하고싶다면!

    > 컬렉션을 통해 데이터를 복제하여 각 컬렉션 일부분에 속하는 데이터를 정확하게 산출

    하지만 `데이터가 중복`되어서 영향을 줍니다. SQL은 데이터가 중복될 일이 없기 때문에 안전합니다.

자주 변경되지 않는 데이터일 때 NoSQL을 쓰면 상당히 효율적이다.

<br>

**확장**

수평적 확장 : 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미 (하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동)

<br>

## 그래서 뭘 쓴다고?

<hr>

### SQL 장점

- 명확하게 정의된 스키마, 데이터 무결성 보장
- 관계는 각 데이터를 중복없이 한번만 저장

### S**QL 단점**

- 덜 유연함. 데이터 스키마를 사전에 계획하고 알려야 함. (나중에 수정하기 힘듬)
- 관계를 맺고 있어서 조인문이 많은 복잡한 쿼리가 만들어질 수 있음
- 대체로 수직적 확장만 가능함

### N**oSQL 장점**

- 스키마가 없어서 유연함. 언제든지 저장된 데이터를 조정하고 새로운 필드 추가 가능
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장됨. 데이터 읽어오는 속도 빨라짐
- 수직 및 수평 확장이 가능해서 애플리케이션이 발생시키는 모든 읽기/쓰기 요청 처리 가능

### N**oSQL 단점**

- 유연성으로 인해 데이터 구조 결정을 미루게 될 수 있음
- 데이터 중복을 계속 업데이트 해야 함
- 데이터가 여러 컬렉션에 중복되어 있기 때문에 수정 시 모든 컬렉션에서 수행해야 함 (SQL에서는 중복 데이터가 없으므로 한번만 수행이 가능)

> 이 때문에 명확하게 정의된 스키마가 있고, 개인 거래내역과 같은 각 데이터를 중복없이 한번만 저장한다는 점에서 우리는 관계형 DB인 SQL을 선택하게 되었습니다.

<br>

자, 그럼 SQL중에서도 postgreSQL을 선택한 이유는 무엇일까요?

결론부터 말하자면 없습니다.

<br>

## PostgreSQL vs MySQL

<br>

![PostgreSQL vs MySQL](https://www.postgresqltutorial.com/wp-content/uploads/2017/02/postgresql-vs-mysql-features.jpg)

<br>

> 1. 하단의 표에서 postgreSQL은 advanced하고 MySQL은 popular라고 하는데 더 이상 둘의 성능 차이는 없다고 봐도 무방하다.

> 2. MVCC(다중 버전 동시성 제어)

    MVCC - 동시에 데이터 작업이 진행되더라도 일단 모든 동작을 기록해두고 가장 마지막 작업 결과가 최종 값으로 인지하게 하는 것
    로킹에 의해 병목이 생기지 않아 `속도 우위`를 가진다.

    다만, Update 시 과거 행을 삭제하고 변경된 데이터를 가진 행을 추가해야해서 MySQL보다 성능이 좋지 않다.

    PostgreSQL과 MySQL 모두 mvcc와 lock을 적절하게 트랜잭션 격리 수준에 따라 동시성 제어를 하고 있다.

    결론: 차이 없다. 땅땅

> 3. Read Committed와 Repeatable Read 수준

### PostgreSQL - Read Committed

    한 읽기 트랜잭션이 시작했을때 다른 트랜잭션은 자유롭게 UPDATE 가능하다.
    한 읽기 트랜잭션은 다른 트랜잭션에서 Update 완료(commit)된 데이터만 조회할 수 있다.
    -> 다른 트랜잭션의 커밋들로 인해 데이터 상태가 계속 변화될 수 있어서 일관되지 못하다.

### MySQL - Repeatable Read

    한 읽기 트랜잭션이 시작했을때 다른 트랜잭션은 자유롭게 UPDATE 가능하다.
    한 읽기 트랜잭션은 자기자신 트랜잭션이 시작한 순간 이전의 데이터 상태로만 조회할 수 있다.
    -> 아무리 트랜잭션의 변경이 일어나도 한 읽기 트랜잭션 내에서 일관된 데이터를 얻을 수 있다.

<br>

## 결론

<hr>

보기엔 MySQL과 postgreSQL이 차이가 없어보인다.

실제로 유의미한 차이를 가질 지 의문이다.

postgreSQL은 우버가 쓰고있는데 자세한 내용은 우버의 RDBMS 사용 방식에 대해 알아보면 좋겠다.

다만 우리 회사는 개발 과정에서 실험적으로 차이를 도출하려고 하고 있다.

<br>

아래의 표는 참고용입니다. 현재의 버전과 다를 수 있습니다.

<hr>

|                                             | PostgreSQL                                                                                                                            | MySQL                                                                                                                                                                                                 |     |     |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- | --- |
| Known as                                    | The world’s most `advanced` open source database.                                                                                     | The world’s most `popular` open source database.                                                                                                                                                      |     |     |
| Development                                 | PostgreSQL is an open source project.                                                                                                 | MySQL is an open-source product.                                                                                                                                                                      |     |     |
| Pronunciation                               | post gress queue ell                                                                                                                  | my ess queue ell                                                                                                                                                                                      |     |     |
| Licensing                                   | MIT-style license                                                                                                                     | GNU General Public License                                                                                                                                                                            |     |     |
| Implementation programming language         | C                                                                                                                                     | C/C++                                                                                                                                                                                                 |     |     |
| GUI tool                                    | PgAdmin                                                                                                                               | MySQL Workbench                                                                                                                                                                                       |     |     |
| ACID                                        | Yes                                                                                                                                   | Yes                                                                                                                                                                                                   |     |     |
| Storage engine                              | Single storage engine                                                                                                                 | Multiple storage engines e.g., InnoDB and MyISAM                                                                                                                                                      |     |     |
| Full-text search                            | Yes                                                                                                                                   | Yes (Limited)                                                                                                                                                                                         |     |     |
| Drop a temporary table                      | No TEMP or TEMPORARY keyword in DROP TABLE statement                                                                                  | Support the TEMP or TEMPORARY keyword in the DROP TABLE statement that allows you to remove the temporary table only.                                                                                 |     |     |
| DROP TABLE                                  | Support CASCADE option to drop table’s dependent objects e.g., tables and views.                                                      | Does not support CASCADE option.                                                                                                                                                                      |     |     |
| TRUNCATE TABLE                              | PostgreSQL TRUNCATE TABLE supports more features like CASCADE, RESTART IDENTITY, CONTINUE IDENTITY, transaction-safe, etc.            | MySQL TRUNCATE TABLE does not support CASCADE and transaction safe i.e,. once data is deleted, it cannot be rolled back.                                                                              |     |     |
| Auto increment Column                       | SERIAL                                                                                                                                | AUTO_INCREMENT                                                                                                                                                                                        |     |     |
| Identity Column                             | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Analytic functions                          | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Data types                                  | Support many advanced types such as array, hstore, and user-defined type.                                                             | SQL-standard types                                                                                                                                                                                    |     |     |
| Unsigned integer                            | No                                                                                                                                    | Yes                                                                                                                                                                                                   |     |     |
| Boolean type                                | Yes                                                                                                                                   | Use TINYINT(1) internally for Boolean                                                                                                                                                                 |     |     |
| IP address data type                        | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Set default value for a column              | Support both constant and function call                                                                                               | Must be a constant or CURRENT_TIMESTAMP for TIMESTAMP or DATETIME columns                                                                                                                             |     |     |
| CTE                                         | Yes                                                                                                                                   | Yes (Supported CTE since MySQL 8.0)                                                                                                                                                                   |     |     |
| EXPLAIN output                              | More detailed                                                                                                                         | Less detailed                                                                                                                                                                                         |     |     |
| Materialized views                          | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| CHECK constraint                            | Yes                                                                                                                                   | Yes (Supported since MySQL 8.0.16, Before that MySQL just ignored the CHECK constraint)                                                                                                               |     |     |
| Table inheritance                           | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Programming languages for stored procedures | Ruby, Perl, Python, TCL, PL/pgSQL, SQL, JavaScript, etc.                                                                              | SQL:2003 syntax for stored procedures                                                                                                                                                                 |     |     |
| FULL OUTER JOIN                             | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| INTERSECT                                   | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| EXCEPT                                      | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Partial indexes                             | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Bitmap indexes                              | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Expression indexes                          | Yes                                                                                                                                   | No                                                                                                                                                                                                    |     |     |
| Covering indexes                            | Yes (since version 9.2)                                                                                                               | Yes. MySQL supports covering indexes that allow data to be retrieved by scanning the index alone without touching the table data. This is advantageous in case of large tables with millions of rows. |     |     |
| Triggers                                    | Support triggers that can fire on most types of command, except for ones affecting the database globally e.g., roles and tablespaces. | Limited to some commands                                                                                                                                                                              |     |     |
| Partitioning                                | RANGE, LIST                                                                                                                           | RANGE, LIST, HASH, KEY, and composite partitioning using a combination of RANGE or LIST with HASH or KEY subpartitions                                                                                |     |     |
| Task Schedule                               | pgAgent                                                                                                                               | Scheduled event                                                                                                                                                                                       |     |     |
| Connection Scalability                      | Each new connection is an OS process                                                                                                  | Each new connection is an OS thread                                                                                                                                                                   |     |     |

[자료 출처: https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-vs-mysql/](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-vs-mysql/)

<hr><br>

[참고: https://uminoh.tistory.com/32#:~:text=%EB%AA%85%ED%99%95%ED%95%9C%20%EC%B0%A8%EC%9D%B4%EB%9D%BC%EA%B3%A0%20%EB%B3%BC%20%EC%88%98,%EB%A5%BC%20%EA%B0%80%EC%A0%B8%EC%98%AC%20%ED%99%95%EB%A5%A0%EC%9D%B4%20%EB%86%92%EB%8B%A4.](https://uminoh.tistory.com/32#:~:text=%EB%AA%85%ED%99%95%ED%95%9C%20%EC%B0%A8%EC%9D%B4%EB%9D%BC%EA%B3%A0%20%EB%B3%BC%20%EC%88%98,%EB%A5%BC%20%EA%B0%80%EC%A0%B8%EC%98%AC%20%ED%99%95%EB%A5%A0%EC%9D%B4%20%EB%86%92%EB%8B%A4.)

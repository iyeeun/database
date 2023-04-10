# DB 정리 1

### Chapter 1 : Introduction

1. Database Systems
    - Database
        
        : Organized collection of inter-related data that models some aspect of the real-world
        
        a collection of relations
        
        cf> 
        
        database schema - the logical structure of the database
        
        database instance - a snapshot of the data in the DB at a given instant in time
        
        relation instance - a snapshot of a relation at a given instant in time
        
    - File System의 단점
        - Data integrity (validity), Implementation, Durability (machine crash)
        - Data redundancy and inconsistency, Difficulty in access data, Data isolation, Integrity problems, Atomicity problems, Concurrent-access anomalies, Security problems
    - Database Management System (DBMS)
        
        : Software that allows applications to store and analyze information in a database
        
        as a data storage (abstraction) / as an interface (DDL+DML)
        

### Chapter 2 : Introduction to the Relational Model

1. Structure of Relational Databases
    - Relational Data Model
        - Data Model
            
            : A notion for describing data or information
            
            Structure, Operations, Constraints로 구성
            
        
        : A data model describes data in terms of relations (tables)
        
    - Relation(table)
        
        = attribute(column, field, variable, feature) + tuple(row, record, data entity, data instance)로 구성
        
    - Key
        - super key
            
            : tuple을 구별, column set 가능
            
        - candidate key
            
            : 최소한의 attribute로 구분할 수 있는 key
            
        - primary key
            
            : candidate key 중에서 하나를 선택
            
            테이블에서 오직 하나, NULL 안됨, 중복값 안됨
            
        - alternate key
            
            : candidate key - primary key
            
        - foreign key
            
            : 다른 relation의 PK tuple과 매핑
            
            referenced data는 그 전에 테이블에 있어야 함 없으면 rejected
            
            NULL 안됨 (PK니까)
            
    - Data Language
        - Data Definition Language (DDL)
            
            : represents relations and information in a DB
            
             defines database schemas (logical structure of DB)
            
        - Data Manipulation Language (DML)
            
            : store and retrieve information from a database
            
            procedural, based on relational algebra
            
        - Data Query Language (DQL)
            
            : DML의 부분, get some schema relation
            
        - Data Control Language (DCL)
            
            : permission 관리 ex) GRANT, REVOKE
            
        - Transaction Control Language (TCL)
            
            : transaction 관리 ex) COMMIT, ROLLBACK, SAVEPOINT, SET TRANSACTION
            
    - Relational Algebra %%%
        
        1) select 
        
        : σ predicate (relation)
        
        SELECT * FROM relation WHERE predicate
        
        predicate 안에 =, <>, >, ≥, <, ≤, and, or, not 가능
        
        2) project
        
        : Π list of attribute (relation)
        
        duplicate rows are removed (모든게 중복이면)
        
        list of attribute이지 predicate이 아니기 때문에 logical operator 쓸 수 없음
        
        3) cartesian product
        
        : relation1 X relation2
        
        combines information
        
        4) join
        
        : r ⋈θ s
        
        relation1 JOIN predicate relation2
        
        select + cartesian product
        
        predicate를 만족하는 tuple을 select
        
        5) rename
        
        6) union
        
        : same arity(attribute)
        
        7) set-intersection
        
        8) set-difference
        

### Chapter 3 : Introduction to SQL

1. Structured Query Language (SQL)
    
    : principal language used to describe and manipulate relational databases
    
    implementation에는 관심 없음, query optimization
    
    - 구성 %%%
        
        1) Data definition : declares DB schemas (DDL)
        
        2) Data manipulation : for querying and modifying the DB (DML)
        
        3) Integrity : 
        
        4) View definition : 
        
        5) Transaction control : 
        
        6) Embedded and Dynamic SQL : 
        
        7) Authorization : 
        
2. DML
    
    1) SELECT, FROM, WHERE clause
    
    1. SELECT 
        
        : lists the attributes (projection)
        
        ALL - default, 중복 제거 안함
        
        DISTINCT - 중복 제거
        
        literal(’’)과 함께 사용하면 FROM 없이 가능
        
        operation에 arithmetic expressions 사용 가능
        
    2. WHERE 
        
        : conditions(predicates)를 지정 (selection)
        
        logical connectives, comparison operators와 함께 사용 가능
        
        - BETWEEN / NOT BETWEEN
            
            : BETWEEN a AND b ↔ [a, b]
            
        - Tuple comparison
    3. FROM
        
        : lists the relations (Cartesian-product)
        
        generates every possible pairs
        
        WHERE과 함께 쓰여 join을 구현
        
    4. AS
        
        : renames relation (rename)
        
        relation AS new_name(correlation name, table alias, correlation variable, tuple variable)
        
    
    2) NULL values
    
    : unknown or does not exist
    
    arithmetic에 null 포함되면 결과는 null
    
    - IS NULL / IS NOT NULL
        
        : 해당 tuple이 NULL 값인지 / 아닌지 체크
        
    - IS UNKNOWN / IS NOT UNKNOWN
        
        : true/false가 아닌 값
        
    
    3) String operations
    
    - Case-sensitive
        
        : upper(s), lower(s), trim(s) 등의 함수 제공
        
    - LIKE
        
        : 패턴 일치 확인
        
        % - substring (null 가능), _ - character
        
    - \ (backslash)
        
        : 특수 문자 사용을 위한 default escape character, ESCAPE ‘’로 다른 문자도 사용 가능 
        
    - etc
        
        : concat(||), length, extracting
        
    
    4) Ordering
    
    - ORDER BY
        
        : tuple이 정렬된 순서로 나타나도록 함 (column 단위, 중복이 있을 때 두 번째 column순으로 정렬)
        
    - ASC, DESC
        
        : 오름차순 (알파벳순) default, 내림차순
        
    
    5) Set operations
    
    : 자동적으로 중복 제거, 중복 유지하려면 ALL 이용
    
    - UNION
        
        : tuple의 합집한 연산, mysql O
        
    - INTERSECT
        
        : 교집합, mysql X
        
        → IN을 이용해 구현
        
    - EXCEPT
        
        : 차집합, mysql X
        
        → NOT IN을 이용해 구현
        
    
    6) Aggregate functions, aggregation
    
    : collection of values를 입력 받아 single value를 반환하는 함수
    
    (ex) AVG, MIN, MAX, SUM, COUNT
    
    - GROUP BY
        
        : 같은 값을 가지는 tuple을 그룹으로 형성
        
        SELECT attributes1 FROM relation GROUP BY attributes2;
        
        aggregate function에 없는데 attributes1에 있으면 attributes2에도 있어야 함
        
    - HAVING
        
        : SELECT attributes1 FROM relation GROUP BY attributes2 HAVING aggregate functions condition;
        
        HAVING에 나타나지 않은 attributes는 GROUP BY에 나타나야 함
        
        WHERE과의 차이점 - WHERE은 grouping 전에, HAVING은 grouping 후에
        
    
    7) Nested subqueries
    
    : subquery
    
    - FROM clause
        
        : any valid subquery
        
    - WHERE clause
        
        : B <operation> (subquery)
        
    - SELECT clause
        
        : scalar subquery
        
    - WITH
        
        : WITH table_name(columns) AS (SUBQUERY) ~~
        
        temporary relation 제공
        
    - Scalar subquery
        
        : single value가 예상되는 query (1X1)
        
        모든 것에 대해 달랑 하나인건 아님 ! 각 조건에 대해 하나도 가능
        
    
    8) Set membership
    
    - IN / NOT IN
        
        : WHERE attributes IN / NOT IN (SET)
        
        뒤의 set에 포함 / 불포함 체크
        
        다른 테이블의 특정한 조건을 만족하는 경우를 체크할 때도 쓰임
        
        tuple-level comparison 가능
        
    - SOME
        
        : WHERE attribute operator SOME (SET)
        
        at least one element가 조건을 만족하는지 체크
        
        IN과 동등
        
    - ALL
        
        : WHERE attribute operator ALL (SET)
        
        모든 element가 조건을 만족하는지 체크
        
        NOT IN과 동등
        
    - EXISTS / NOT EXISTS
        
        : WHERE EXISTS / NOT EXISTS (SET)
        
        subquery의 결과가 nonempty / empty이면 true를 반환
        
    - UNIQUE
        
        : WHERE UNIQUE (SET)
        
        중복 없는지 확인, but mysql X
        
3. DDL
    
    : 아래의 세 키워드는 storage를 건듦
    
    1) Commands
    
    (1) INSERT
    
    : INSERT INTO table VALUES(value_list)
    
    table schema와 같은 순서, 다르게 할 거면 table 뒤에 column list 써야함
    
    적지 않은 value는 null or default value로 처리
    
    string ‘’, case-sensitive
    
    SELECT query의 결과를 먼저 처리하여 삽입할 수 있음
    
    (2) UPDATE
    
    : UPDATE table SET column=value (WHERE predicate)
    
    조건 거는 순서 중요
    
    CASE clause 이용할 수 있음
    
    - CASE
        
        : CASE WHEN condition1 THEN statement1 ELSE statement2 END
        
    
    (3) DELETE
    
    : DELETE FROM table WHERE predicate
    
    foreign key로 쓰이는 테이블은 지울 수 없음
    
    전체 rows 삭제 - TRUNCATE (TABLE) table → structure은 남고 데이터만 없어짐
    
    cf>
    
    DELETE : 공간은 남아있음
    
    TRUNCATE : 공간은 사라지고 헤더만 남음
    
    DROP : schema까지 전부 사라짐
    
    (4) ALTER
    
    : table schema 바꾸기
    
    ALTER TABLE table ADD attribute data_type
    
    ALTER TABLE table MODIFY attribute data_type
    
    ALTER TABLE table DROP attribute
    
    (5) Table commands
    
    - CREATE DATABASE database_name
    - USE database_name
    - CREATE TABLE table_name ( columns data_type[size], ... )
    - integrity constraint
        
        : %%%
        
        - PRIMARY KEY (attribute_set)
        - FOREIGN KEY (attribute_set) REFERENCES relation
        - UNIQUE (attribute_set)
            
            → candidate key
            
            - PRIMARY KEY vs. UNIQUE
                
                : 의미는 중복이 없어야 한다는 점→각 row를 구별한다는 점에서 공통점을 가짐
                
                차이점
                
                - NULL 받을 수 없음 / 있음
                
                - relation 당 하나 / 여러개 가능
                
                - clustered index / non-clustered index
                
        - att NOT NULL
        - CHECK (constraint)
        - DEFAULT
    
    2) Domain Types
    
    1) string
    
    - CHAR(n) : 길이 고정, [0, 255]
    - VARCHAR(n) : 길이 변함, [0, 65535], 마지막에 NULL 가짐 → 1 byte 추가적으로 필요, 길이 n인 문자열도 저장하는지는 DB엔진 따라 다름
    - TEXT : varchar보다 긺 → large object (BLOB) ??
        - TINYTEXT [0, 255], TEXT [0, 65535], MEDIUMTEXT [0, 16777215], LONGTEXT [0, 4294967295]
    
    2) numeric
    
    - INT : 4 bytes
    - SMALLINT : 2 bytes
    - BIGINT : 8 bytes
    - TINYINT(1), MEDIUMINT(3) : depending on DBMS
    - NUMERIC(p, d) : fixed point number, p digits /w d digits to the right of decimal point → DECIMAL in mysql
    - FLOAT : single-precision
    - REAL, DOUBLE : double-precision
    
    3) temporal
    
    - DATE : YYYY-MM-DD
    - TIME : HH:MM:SS
    - DATETIME : DATE + TIME
    - YEAR : YYYY
    - TIMESTAMP(n) : UNIX time since 1970, n에 따라 패턴 바뀜 (size가 바뀌는 건 아님)
    
    4) large objects
    
    - BINARY(n) : fixed length binary
    - VARBINARY(n) : variable length binary
    - BLOB(n) : Binary Large OBject data type, TINY, MEDIUM, LONG ~

### Chapter 6 : Database Design Using the E-R Model

1. Designing a database
    
    1) Design Phases
    
    1. Initial : data needs
    2. Second : choose a data model
    3. Final : implementation
2. E-R diagrams
    
    1) Entity Relationship Model
    
    - entity - a set of attributes, thing or object
    - relationship - association
    
    2) E-R diagrams
    
    - diagram
        - rectangle - entity sets
        - attributes - inside rectangle
        - underline - primary key attributes
        - diamond - relation
        - 점선 - discriminator in weak entity
        - diamond에 연결된 attribute - relation attribute
    - attribute types
        - simple ↔ composite
            
            : subpart로 나눠질 수 있는지
            
            composite - indent하여 sub-attribute 기술
            
        - single-valued ↔ multivalued
            
            : 여러 값을 가질 수 있는지
            
            multivalued - { }
            
        - derived
            
            : 다른 attribute로부터 계산 가능한지
            
            ()
            
    - Mapping cardinalities
        - one to one
        - one to many
        - many to one
        - many to many

### Chapter 7 : Relational Database Design

1. Decomposition
    
    : relational schema의 디자인에 따라 성능이 달라져서 
    
    - 문제점
        - repetition of data
        - data consistency issues
            
            : insertion anomaly (넣을 때 불필요한 정보도 같이), deletion anomaly (관련된 데이터에 의해 소실), update anomaly (수정될 때 다른 데이터도 수정되어야 함)
            
    - Lossy decomposition
        
        : a decomposition from which the original relation cannot be reconstructed
        
        정보는 더 많이 생기지만 원래 관계를 알 수 없게 됨
        
        원래 관계의 superset이 됨
        
2. Normal Form
    
    : data redundancy 감소 & data integrity 향상를 위해
    
    1) 1NF
    
    : atomic values
    
    column name 중복 없어야 함, atomic data type, data domain이 같아야 함, 순서 상관 없음, 중복 없어야 함
    
    2) 2NF
    
    : partial dependency 없앰
    
    part of PK → non-PK (X)
    
    3) 3NF
    
    : transitive dependency 없앰
    
    non-PK → non-PK (X)
    
    4) BCNF (3.5NF, Boyce-Codd)
    
    : 3NF에 candidate key 여러개이면
    
    For any dependency A→B, A should be a super key (unique)
    
    A→B and A is non-PK (X)
    
    non-PK → PK
    
    5) 4NF
    
    : multi-valued dependency 없앰 (independent X)
    
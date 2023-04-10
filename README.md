# Database

## Database Systems (22-1 수강)
### 내용 정리
- [DB 수업 정리 1](./study/db1.md)
- [DB 수업 정리 2](./study/db2.md)

### 과제 정리
#### [Term project](./assignment/)
- 문제 : 주어진 데이터를 분석하여 DB 설계하고 최적화하기
- 접근 방법
    - 테이블 설계 및 관계 정의 - ER diagram 그리기
    - Normalization을 통해 DB 나누기
    - Denormalization 수행 - JOIN으로 인한 cost가 큰 경우
    - Index 정의
    - 설계 내용 justification
- 내 역할 + 어려웠던 점
    - Normalization 수행 : 중복된 데이터를 줄이고 테이블을 작게 가져가는 것과 JOIN으로 인한 부하를 줄이는 것 중 어느 것이 적절한지 판단해야 함
    - 쿼리 작성 : 원하는 결과를 얻을 수 있도록 쿼리를 작성해야 함. 인덱스를 사용하는 경우와 그렇지 않은 경우의 결과를 비교하며 어떤 인덱스가 효과적인지 파악하는 것이 필요. 성능 개선을 기대하고 수행한 인덱스가 그렇지 않은 경우가 간혹 있어 그 이유를 찾고 다른 개선점을 찾는 과정이 어려웠음. 

#### [개인 과제](./assignment/)
- HW 1
    - Relational Algebra의 표현 방식 이해

- HW 2
    - 기본적인 DML을 이용하여 MySQL 쿼리 작성

- HW 3
    - ER diagram, DDL, Normalization에 대한 이해

- HW 4
    - GROUP 연산, WINDOW 연산을 이용한 DML 쿼리 작성, Transaction에 대한 이해

- HW 5
    - Index와 Index의 원리에 대한 이해 및 쿼리 작성

## SQLD (23-1 취득)
### 내용 정리
- [SQLD 준비 정리 내용](./study/sqld.md)
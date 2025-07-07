## 1장 질문지

## 1. 데이터베이스의 수평적 확장은 샤딩이라고도 부르는데 더 많은 서버를 추가함으로써 성능을 향상시킬 수도 있다고한다. 노션에서 진행한 sharding 방식을 이용하면 수평적, 수직적 확장이 가능할까?
- [notion sharding](https://www.notion.com/blog/sharding-postgres-at-notion)
![image](https://github.com/user-attachments/assets/3c98fe43-0e63-4469-a641-ec69275cfa01)




## 2. p4 ~ p5를 보면 nosql이 유리한 경우가 제시되어 있는데 관계형 데이터베이스가 유리한 경우는 어떤게 있는가?

---

## 관계형 데이터베이스 vs NoSQL 비교표 by claude

| 구분 | 관계형 데이터베이스 (RDBMS) | NoSQL |
|------|---------------------------|-------|
| **데이터 구조** | 테이블 기반 (행과 열) | 다양한 구조 (문서, 키-값, 컬럼, 그래프) |
| **스키마** | 고정된 스키마 필요 | 유연한 스키마 또는 스키마 없음 |
| **확장성** | 수직 확장 (Scale-up) | 수평 확장 (Scale-out) |
| **ACID 속성** | 강한 ACID 지원 | 제한적 ACID 지원 (BASE 모델) |
| **일관성** | 강한 일관성 (Strong Consistency) | 최종 일관성 (Eventual Consistency) |
| **쿼리 언어** | SQL (표준화된 언어) | 각 데이터베이스별 고유 API |
| **조인 연산** | 복잡한 조인 연산 지원 | 제한적 조인 지원 |
| **트랜잭션** | 강력한 트랜잭션 지원 | 제한적 트랜잭션 지원 |
| **성능** | 복잡한 쿼리에 최적화 | 단순한 읽기/쓰기에 최적화 |
| **데이터 무결성** | 참조 무결성 보장 | 애플리케이션 레벨에서 관리 |

## 주요 예시

### 관계형 데이터베이스
- MySQL: 가장 널리 사용되는 오픈소스 RDBMS
- PostgreSQL: 고급 기능을 제공하는 객체-관계형 데이터베이스
- Oracle: 엔터프라이즈급 상용 데이터베이스
- SQL Server: 마이크로소프트의 관계형 데이터베이스

### NoSQL 데이터베이스
- 문서형: MongoDB, CouchDB
- 키-값: Redis, DynamoDB
- 컬럼형: Cassandra, HBase
- 그래프형: Neo4j, Amazon Neptune
---  

## 3. 부서에서 주로 사용하는 캐시를 위한 데이터베이스를 어떤것을 사용하는가?
- ex) redis, local, ...

# 데이터베이스 모니터링 및 최적화 개요

## 데이터베이스 모니터링

데이터베이스 시스템의 성능, 상태, 자원 사용량 등을 지속적으로 감시하고 분석하는 과정

데이터베이스의 실시간 운영 상태를 파악하기 위해 다양한 도구와 기술을 사용하여 주요 성능 지표를 추적

### 모니터링 목적

이벤트와 로그 수집 및 분석으로 잠재적 문제를 조기에 발견하고 대응

실시간 알림 설정으로 성능 저하, 장애 발생 시 신속 대응

장기적 성능 데이터를 기반으로 시스템 트렌드를 분석하고 성능 최적화 및 확장 계획 수립

## 데이터베이스 최적화

데이터베이스 시스템 성능을 향상시키기 위해 구조, 쿼리,  인덱스 등을 개성하는 과정

자원 사용을 효율적으로 관리하고 응답 속도를 단축시켜 사용자 경험을 향상시키며 운영 비용을 절감

### 최적화의 목적

쿼리 성능을 향상시키기 위해 인덱스를 추가하거나 조정하고 비효율적인 쿼리 재작성

테이블을 정규화 또는 비정규화하여 접근 속도 개선

데이터 분할 및 아카이빙으로 큰 데이터 관리

캐싱을 통해 반복 접근 속도를 높이고 시스템 자원의 사용 최적화

## 데이터베이스 모니터링과 최적화

모니터링으로 수집된 데이터는 최적화의 기반

모니터링은 최적화 후 효과 검증 역할도 함

지속적 모니터링으로 최적화 효과를 유지하고 새로운 성능 문제를 조기 해결 가능

모니터링으로 문제를 발견하고 최적화로 문제 해결

## 데이터베이스 모니터링 최적화 사례

### 1. 알람을 통해 데이터베이스 문제 상황 전파

- 데이터베이스 저장 용량이 95% 이상 사용된다고 알람이 옴

### 2. 문제 원인 파악

- 컬렉션 내 전체 문서를 검색하는 COLLSCAN 쿼리가 실행되고 있었음

### 3. 문제 해결

- 인덱싱 설정 및 앱 내 쿼리 최적화
- 먄약 인덱싱 및 쿼리 최적화로 문제 해결을 하지 못했다면 데이터베이스 Scale-Up 필요

## 쿼리가 점점 느려지는 이유

### 데이터 양 증가

- 테이블 데이터가 늘어나며 쿼리 처리 시간이 길어짐
- 인덱스가 커져 검색 속도 저하

### 자원 사용 경쟁

- 동시에 실행되는 쿼리와 작업이 늘어나며 CPU, 메모리, 디스크 I/O 등의 자원 경쟁 발생
- 잠금 경합으로 인해 쿼리 처리 속도가 느려짐

### 앱 변경

- 앱 코드가 변경되며 쿼리 호출 빈도나 방식이 바뀔 수 있음
- 새로운 기능이 추가되며 시스템 부하 증가 가능

### → 모니터링으로 문제 사전 방지가 중요

# 데이터베이스 모니터링

## 모니터링할 지표

### CPU 사용량

데이터베이스는 CPU를 이용하여 쿼리 처리와 데이터 연산을 수행하므로 과도한 CPU 사용은 성능 저하를 초래할 수 있으며 서버의 과부하 상태를 파악하고 조치를 취하는 것이 중요

### 메모리 사용량

데이터베이스는 데이터 캐싱과 쿼리 실행시 메모리를 사용하므로 메모리 부족은 쿼리 성능 저하와 시스템 불안정 유발

### 디스크 I/O

데이터베이스의 읽기 및 쓰기 작업은 디스크 I/O에 의존하므로 디스크 I/O 성능이 낮으면 데이터 접근 속도가 느려지고 전체 시스템 성능에 영향

### 네트워크 트래픽

데이터베이스 서버와 클라이언트 간 데이터 전송이 네트워크를 통해 이뤄지므로 네트워크 트래픽이 과도하면 데이터 전송 속도가 저하되고 응답 시간이 길어짐

### 쿼리 실행 시간

쿼리 실행 시간이 긴 슬로우 쿼리는 성능 문제를 야기

슬로우 쿼리를 모니터링하고 분석하여 비효율적인 쿼리와 인덱스 문제를 발견하고 최적화해야함

## 모니터링할 로그

### 에러 로그

- 목표: 에러 로그를 통해 시스템 장애, 예외 상황, 오류 발생 원인 파악
- 내용: 시스템 오류, 쿼리 실패, 연결 문제 등
- 도구: 데이터베이스 관리 도구에서 제공하는 에러 로그 뷰어

### 접속 로그

- 목표: 데이터베이스 접근 패턴 분석, 비정상적 접근 시도 탐지
- 내용: 사용자 로그인, 접속 시간, 접속 IP 주소
- 도구: 데이터베이스 접속 로그 기능, 보안 모니터링 도구

### 백업 로그

- 목표: 백업 작업의 성공 여부 확인, 백업 주기 및 상태 모니터링
- 내용: 백업 시작 및 종료 시간, 백업 성공/실패 여부
- 도구: 데이터베이스 백업 관리 도구, 백업 로그 분석 도구

## 주요 모니터링 도구 및 기술

### MySQL Profiling

MySQL에서 제공하는 기본 프로파일링 기능을 통해 SQL 구문에서 병목 지점을 찾을 수 있음

```python
-- 1. OFF가 기본값이므로 프로파일링을 하기 위해서 ON 으로 설정
SET profiling = 'ON';

-- 2. 프로파일링 할 SQL 구문 실행
SELECT * FROM employee WHERE employee_id = 100000;

-- 3. 프로파일링된 쿼리 목록 확인
SHOW PROFILES;

-- 4. 특정 쿼리에 대한 상세 프로파일링 내용 확인
SHOW PROFILE FOR QUERY 1;
```

![image](https://github.com/user-attachments/assets/89236c8e-6d8b-4958-9191-959708966150)

### MySQL Slow Query Logging

수행시간이 오래 걸리는 쿼리를 로그로 남길 수 있음

슬로우 쿼리 로깅을 설정하려면 my.cnf 파일을 아래와 같이 설정

```sql
[mysqld]

# 슬로우 쿼리를 TABLE로 출력한다. FILE로도 설정할 수 있다
# FILE로 설정했다면 slow_query_log_file로 출력할 파일 위치를 설정할 수 있다
log_output = TABLE

# 슬로우 쿼리 활성화
slow_query_log = 1

# 아래 변수에 지정된 초(seconds)이상 쿼리가 수행되면 슬로우 쿼리에 기록된다
long_query_time = 1
```

- 코드 실행

```sql
-- 1. 쿼리 실행
SELECT COUNT(*) FROM employees;

-- 2. 슬로우 쿼리 로그 조회
SELECT * FROM mysql.slow_log;

-- start_time: 쿼리가 시작된 시간
-- user_host: 쿼리를 실행한 사용자
-- query_time: 쿼리가 실행되는 데 걸린 시간
-- lock_time: 테이블 잠금에 대한 대기 시간
-- rows_sent: 실제 클라이언트에 전달된 레코드의 수
-- rows_examined: 쿼리가 처리되기 위해 실제 접근한 레코드의 수
-- db: 쿼리가 수행된 데이터베이스
-- sql_text: 실제 수행된 쿼리
```

![image](https://github.com/user-attachments/assets/832dc25b-0198-42b6-a7d8-e3dee82a1471)

### MySQL Workbench

MySQL 데이터베이스의 설계, 관리, 모니터링을 위한 통합 도구

쿼리 성능 분석, 모니터링 등 다양한 기능 제공

- 성능 모니터링
    - Performance Dashboard
        - 기능: 서버 주요 성능 지표를 실시간으로 시각화
        - 모니터링 항목: CPU 사용량, 메모리 사용량, 디스크 I/O, 쿼리 성능
        - 장점: 직관적인 대시보드, 실시간 상태 파악
    - Server Status
        - 기능: MySQL 서버의 상태 정보를 제공
        - 모니터링 항목: 연결 수, 쿼리 처리량, 캐시 히트율 등
        - 장점: 상세한 서버 상태 정보 제공, 성능 병목 식별
- 쿼리 성능 분석
    - Query Analyzer
        - 기능: 실행 중인 쿼리 성능 분석 및 최적화
        - 모니터링 항목: 쿼리 실행 시간, 읽기/쓰기 작업, 인덱스 사용 현황
        - 장점: 쿼리 성능 무넺 식별, 실행 계획 분석

### MongoDB explain

쿼리 실행 계획을 분석하여 쿼리가 어떻게 실행되는지 보여줌

쿼리 성능을 이해하고 인덱스 사용 여부 및 쿼리 최적화 가능성 파악 가능

```sql
db.collection.find(query).explain("executionStats");
```

- 쿼리 최적화: 쿼리 실행 계획을 분석하여 인덱스를 추가하거나 쿼리를 변경하여 성능 개선 가능
- 인덱스 사용 확인: 쿼리가 예상대로 인덱스를 사용하는지 여부 확인 가능
- 성능 문제 식별: 쿼리 실행 시간이나 문서 검사량이 많은 경우 쿼리 최적화 필요성 확인 가능

### MongoDB Compass

MongoDB 공식 GUI 도구로 데이터베이스의 시각적 관리와 분석 지원

- 쿼리 성능 분석: Explain Plan
    - 기능: 쿼리 실행 계획 시각적 분석
    - 모니터링 항목: 쿼리 실행 경로, 인덱스 사용 여부, 쿼리 성능 통계
    - 장점: 쿼리 최적화 기회 발견, 성능 문제 식별
- 성능 모니터링: Performance Metrics
    - 기능: 서버 성능 지표 모니터링
    - 모니터링 항목: CPU 사용량, 메모리 사용량, 디스크 I/O
    - 장점: 실시간 성능 모니터링, 병목 현상 식별

### MongoDB Atlas Monitoring

MongoDB의 클라우드 데이터베이스 플랫폼인 MongoDB Atlas에서 제공하는 모니터링 서비스

클라우드 기반의 MongoDB 인스턴스를 실시간으로 모니터링하고 성능 분석

- 실시간 성능 모니터링
    - Metrics Dashboard
        - 기능: CPU 사용량, 메모리 사용량, 디스크 I/O, 네트워크 트래픽 등의 성능 지표를 실시간으로 시각화
        - 모니터링 항목: CPU 및 메모리 사용량, 디스크 공간, 네트워크 대역폭
        - 장점: 실시간 데이터 제공, 성능 추세 모니터링
    - Performance Insights
        - 기능: 데이터베이스의 성능에 대한 심층적인 인사이트 제공
        - 모니터링 항목: 쿼리 성능, 데이터베이스 응답 시간, 자원 사용 패턴
        - 장점: 성능 병목 문제 식별, 최적화 기회 발견
- 쿼리 성능 분석
    - Query Performance Monitoring
        - 기능: 실행 시간이 긴 쿼리와 자주 실행되는 쿼리 분석
        - 모니터링 항목: 쿼리 실행 시간, 쿼리 빈도, 인덱스 사용 여부
        - 장점: 성능 문제 해결, 쿼리 최적화 지원
    - Slow Queries
        - 기능: 느리게 실행되는 쿼리를 식별하고 분석
        - 모니터링 항목: 슬로우 쿼리 로그, 쿼리 성능 통계
        - 장점: 쿼리 성능 문제 식별, 개선 방안 제시

## 모니터링 알람

시스템 성능 지표나 상태가 설정된 임계값을 초과할 때 자동으로 경고 알림을 보냄

### 알람 조정 및 최적화

- 경고 레벨 설정: 경고 심각도에 따라 다양한 레벨 설정 (정보, 경고, 심각)
- 알람 빈도 설정: 동일 알람의 빈도를 조정하여 과도한 경고 방지
- 알람 필터링: 중요도가 낮은 알람을 필터링하여 불필요한 경고 줄이기

# 데이터베이스 최적화

## 다양한 쿼리

데이터를 조회할 때는 여러 쿼리 방법이 존재하고 효율적인 쿼리를 사용하면 성능 개선과 자원 사용을 줄일 수 있음

최적화된 쿼리는 데이터베이스 응답 속도를 빠르게 하고 시스템 자원을 절약

### 효율적 쿼리 사용의 중요성

- 성능 향상
- 자원 사용 감소
- 응담 시간 단축
- 운영 비용 절감

## 인덱스 활용

- 비효율적 쿼리: 전체 테이블을 스캔하는 쿼리

```sql
SELECT * FROM orders WHERE customer_id = 123;
```

- 효율적 쿼리: 인덱스를 활용한 쿼리

```sql
CREATE INDEX idx_customer_id ON orders (customer_id);

SELECT * FROM orders WHERE customer_id = 123;
```

## 조인 최적화

- 비효율적 쿼리: 불필요한 조인 사용

```sql
SELECT o.order_id, c.customer_name
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN products p ON o.product_id = p.product_id;
```

- 효율적 쿼리: 필요한 조인만 사용

```sql
SELECT o.order_id, c.customer_name
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id;
```

## 서브쿼리 최적화

- 비효율적 쿼리: 서브쿼리를 사용하여 반복적인 조회

```sql
SELECT order_id
FROM orders
WHERE customer_id IN (SELECT customer_id FROM customers WHERE city = 'New York');
```

- 효율적 쿼리: 조인을 사용하여 서브쿼리 제거

```sql
SELECT o.order_id
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
WHERE c.city = 'New York';
```

## 인덱싱

![image](https://github.com/user-attachments/assets/571d619c-1a00-4de0-b932-29c755ad0da4)

데이터베이스에서 테이블의 특정 컬럼에 대한 인덱스를 생성하여 데이터 검색 속도를 향상시키는 기법

일반적으로 B-트리 또는 해시 구조를 사용하여 데이터 검색 시 빠르게 접근할 수 있도록 함

장점

- 테이블 전체를 스캔하지 않고 빠르게 검색 가능
- 조회 쿼리 성능을 크게 개선
- 정렬(ORDER BY) 및 집계 작업(GROUP BY)의 성능 향상

단점

- 인덱스는 추가 디스크 공간 사용
- 데이터 삽입, 삭제, 수정 시 인덱스도 갱신해야하므로 쓰기 성능에 영향
- 인덱스가 많아지면 관리 및 유지보수 복잡

## 인덱스 생성 예시

- MySQL

```sql
-- 단일 컬럼 인덱스 생성
CREATE INDEX idx_customer_id ON orders (customer_id);

-- 복합 인덱스 생성
CREATE INDEX idx_order_date_customer ON orders (order_date, customer_id);
```

- PostgreSQL

```sql
-- 단일 컬럼 인덱스 생성
CREATE INDEX idx_customer_id ON orders (customer_id);

-- 복합 인덱스 생성
CREATE INDEX idx_order_date_customer ON orders (order_date, customer_id);
```

- MongoDB

```sql
db.collection.createIndex({ customer_id: 1 });
```

## 인덱스 종류

### 단일 컬럼 인덱스

- 하나의 컬럼에 인덱스를 생성
- 단일 컬럼에 대한 검색 성능 개선
- 복합 쿼리나 다중 컬럼 검색 시 성능이 제한적

### 복합 인덱스

- 여러 컬럼을 포함하는 인덱스
- 여러 컬럼을 동시에 검색할 때 성능 개선
- 여러 컬럼을 포함하여 디스크 공간을 더 많이 사용

### 풀텍스트 인덱스

- 텍스트 검색을 최적화하기 위해 문서 내 텍스트를 인덱싱
- 인덱스 순서에 따라 데이터가 정렬되어 있어 범위 검색이 효율적
- 텍스트 인덱스는 상대적으로 큰 디스크 공간 소모

## 인덱스에 따른 쿼리

- 단일 컬럼 인덱스가 적용된 컬럼에 대해 효율적으로 검색

```sql
-- 고객 ID에 단일 컬럼 인덱스가 있는 경우
SELECT * FROM orders WHERE customer_id = 123;

```

- 복합 인덱스가 적용된 경우 인덱스의 첫 번째 컬럼을 WHERE 절의 조건으로 사용해야 최적화

```sql
-- order_date와 customer_id에 복합 인덱스가 있는 경우
SELECT * FROM orders
WHERE order_date = '2024-01-01' AND customer_id = 123;

-- 잘못된 쿼리
SELECT * FROM orders
WHERE customer_id = 123 AND order_date = '2024-01-01';
```

## 비정규화를 통한 성능 개선

조인 연산을 최소화

- 정규화: 데이터 중복을 줄이고 데이터 무결성을 유지하기 위해 데이터를 여러 테이블로 나누는 과정
- 비정규화: 성능 향상을 위해 정규화된 데이터를 의도적으로 중복 저장하거나 합치는 과정

```sql
CREATE TABLE customer_orders AS
SELECT c.customer_id, c.name, c.email, o.order_id, o.order_date
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id;
```

- 조회 성능 향상: 자주 조회되는 데이터를 한 테이블에 저장하여 조인 연산을 줄입
- 쿼리 복잡성 감소: 복잡한 조인 연산을 줄여 쿼리 작성과 실행을 단순화함

### 장점

- 성능 향상
- 쿼리 간소화
- 자원 절약

### 단점

- 데이터 중복 저장
- 데이터 무결성 유지 복잡
- 데이터 업데이트 복잡

## 쿼리 캐싱

자주 실행되는 쿼리의 결과를 저장하고 동일 쿼리가 다시 실행될 때 저장 결과를 즉시 반환하여 성능 개선

### 작동 원리

- 쿼리 실행 결과를 메모리나 디스크에 저장
- 동일 쿼리 요청 시 캐시 사용
- 데이터 변경 발생 시 관련 캐시 무효화 또는 갱신

### 쿼리 캐싱 설정

- MySQL: query_cache_size와 query_cache_type 설정으로 활성화

```sql
SET GLOBAL query_cache_size = 1048576; -- 1MB 캐시 크기 설정
SET GLOBAL query_cache_type = ON; -- 쿼리 캐시 활성화
```

- Redis/Memcached: 메모리 기반 캐시 시스템에 쿼리 결과 저장

```sql
const redis = require("redis");
const client = redis.createClient();

async function cacheQueryResult(queryKey, fetchData) {
    return new Promise((resolve, reject) => {
        client.get(queryKey, async (err, cachedResult) => {
            if (err) return reject(err);
            if (cachedResult) return resolve(JSON.parse(cachedResult));

            try {
                const result = await fetchData();
                client.setex(queryKey, 3600, JSON.stringify(result)); // 1시간 캐시
                resolve(result);
            } catch (error) {
                reject(error);
            }
        });
    });
}

// 사용 예시
(async () => {
    const fetchData = async () => ({ data: "example data" });

    const result = await cacheQueryResult("some_query_key", fetchData);
    console.log(result);
})();
```

## 쿼리 최적화 모범 사례

### 쿼리 리팩토링

- 서브쿼리 대신 조인 사용이나 불필요한 서브쿼리 제거
- SELECT * 대신 필요한 컬럼만 선택하여 성능 개선

### 쿼리 재사용

- 자주 사용하는 쿼리를 최적화하여 재사용
- 이러한 재사용 쿼리를 캐싱하여 시스템 성능 개선

### 인덱스 최적화

- 쿼리에서 자주 검색되는 컬럼, 정렬, 조인 조건에 대해 인덱스 생성
- 여러 컬럼을 동시에 검색하는 경우 복합 인덱스 사용

### 쿼리 분석

- EXPLAIN 명령어를 사용하여 쿼리 실행 계획을 분석하고 최적화

### 데이터베이스 설계 최적화

- 데이터베이스를 필요에 따라 비정규화하여 성능 개선
- 데이터 모델을 설계할 때 적절한 데이터 타입과 길이를 사용하여 저장 공간과 성능 최적화

## 쿼리 최적화의 한계

- 과도한 인덱스 사용
- 복잡한 쿼리에서 인덱스의 비효율성
- 데이터베이스 자체 구조나 성능의 한계
- 하드웨어 자원의 제약

## 데이터베이스 구조 최적화: 파티셔닝

![image](https://github.com/user-attachments/assets/a6942599-14ef-4e38-8438-4ba4a1b375ac)

큰 테이블을 작은 부분으로 나눠 검색 및 쿼리 성능 개선

### 적용 사례

- 로그 데이터: 시간 기반의 로그 데이터를 날짜별로 파티셔닝하여 성능 최적화
- 대규모 사용자 데이터: 사용자 ID를 해시하여 분산 저장함으로 검색 성능 개선

### 장점

- 쿼리 성능을 향상시키고 대규모 데이터의 검색 속도 향상
- 파티션 단위로 데이터 백업 및 복구가 가능하여 관리가 용이

### 단점

- 파티션이 많아질수록 관리 복잡
- 잘못된 파티셔닝 전략은 성능 저하의 원인

### 파티셔닝의 종류

- 범위 파티셔닝
    - 데이터를 날짜나 숫자 범위에 따라 나눠 성능 개선
    - 예를 들어 주문 데이터를 연도별로 파티셔닝하여 쿼리 속도를 높일 수 있음
    
    ```sql
    CREATE TABLE orders (
        order_id INT,
        order_date DATE,
        PRIMARY KEY (order_id, order_date)
    ) PARTITION BY RANGE (YEAR(order_date)) (
        PARTITION p2023 VALUES LESS THAN (2024),
        PARTITION p2024 VALUES LESS THAN (2025),
        PARTITION p2025 VALUES LESS THAN (2026)
    );
    ```
    
- 리스트 파티셔닝
    - 특정 값 목록을 기준으로 데이터를 분할하여 효율적으로 관리
    - 예를 들어 제품 카테고리에 따라 데이터를 나눠 카테고리 별로 빠르게 조회
    
    ```sql
    CREATE TABLE products (
        product_id INT,
        category VARCHAR(50),
        PRIMARY KEY (product_id)
    ) PARTITION BY LIST (category) (
        PARTITION p_electronics VALUES IN ('Electronics'),
        PARTITION p_furniture VALUES IN ('Furniture'),
        PARTITION p_clothing VALUES IN ('Clothing')
    );
    ```
    
- 해시 파티셔닝
    - 해시 함수를 사용하여 데이터를 균등하게 나눠 쿼리 성능 개선
    - 예를 들어 사용자 ID를 해시하여 데이터 분산
    
    ```sql
    CREATE TABLE users (
        user_id INT,
        name VARCHAR(100),
        PRIMARY KEY (user_id)
    ) PARTITION BY HASH (user_id) PARTITIONS 4;
    ```
    
- 키 파티셔닝
    - 데이터베이스 기본 키 값을 해시 함수로 사용하여 파티셔닝
    - 예를 들어 주문 ID를 시준으로 데이터 분할
    
    ```sql
    CREATE TABLE orders (
        order_id INT,
        order_date DATE,
        PRIMARY KEY (order_id)
    ) PARTITION BY KEY (order_id) PARTITIONS 4;
    ```
    

## 아카이빙

오래된 데이터나 사용하지 않는 데이터를 별도의 저장소에 보관하여 현재 데이터베이스 시스템에서 성능을 유지하고 저장 공간을 절약하는 과정

아카이빙된 데이터는 일반적으로 조회 빈도가 낮지만 법적 요구 사항이나 향후 분석 필요성에 따라 보존됨

### 목표

- 데이터 베이스 크기를 줄여 쿼리 성능 유지 및 데이터베이스 관리의 복잡성을 줄임
- 저장 공간 절약
- 법적 요구 사항 준수
- 데이터 복구 및 분석

### 아카이빙 방법

- 파일 기반 아카이빙: 데이터베이스에서 데이터를 파일로 내보내어 저장, 주기적으로 스냅샷을 생성하고 이를 파일 시스템이나 클라우드 스토리지에 보관
    - 예시: Mysqldump를 사용하여 MySQL 데이터베이스의 백업 파일 생성
    
    ```sql
    mysqldump -u username -p database_name > archive_file.sql
    ```
    
- 데이터베이스 아카이빙: 아카이빙 전용 데이터베이스를 구축하거나 기존 데이터베이스의 아카이빙 테이블을 생성하여 데이터 이동
    - 예시: 오래된 데이터를 archive 테이블로 이동
    
    ```sql
    INSERT INTO archive_table SELECT * FROM main_table WHERE date < NOW() - INTERVAL 1 YEAR;
    DELETE FROM main_table WHERE date < NOW() - INTERVAL 1 YEAR;
    ```
    
- 데이터베이스 파티셔닝과 아카이빙: 데이터를 파티셔닝하여 아카이빙 전략을 결합, 예를 들어 날짜 기준으로 데이터를 파티셔닝하여 오래된 파티션을 아카이빙
    - 예시: 날짜 기반 파티셔닝을 설정하고 오래된 파티션 백업
    
    ```sql
    ALTER TABLE orders DROP PARTITION p_old_data;
    ```
    
- 클라우드 스토리지 활용: AWS S3, Azure Blob Storage, Google Cloud Storage 등의 클라우드 스토리지에 데이터를 저장하여 장기 보존 및 관리
    - 예시: AWS S3에 파일 업로드
    
    ```sql
    aws s3 cp archive_file.sql s3://my-bucket/archives/
    ```
    

## 아카이빙 전략

- 정책 정의: 아카이빙 정책을 수립하여 어떤 데이터를 언제, 어떻게 아카이빙할지 결정
    - 데이터 선택 기준, 아카이빙 주기, 아카이빙 저장소, 데이터 보존 기간
    - 모니터링 및 유지보수, 백업 및 복구 계획, 보안 및 접근 제어
- 테스트 및 검증: 아카이빙 전략을 구현하기 전 테스트하여 데이터의 정확성과 복구 가능성 검증
- 모니터링 및 유지보수: 아카이빙 작업의 성과를 모니터링하고 필요에 따라 조정, 지속적으로 아카이빙 전략을 평가하고 개선

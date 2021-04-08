# 응용 SQL 작성
## 집계성 SQL 작성 [ ★★★ ]
### 데이터 분석 함수 
- 총합, 평균 등의 데이터 분석을 위해 복수 행 기준의 데이터를 모아서 처리하는 것을 목적으로 하는 다중 행 함수
- GROUP BY 구문을 활용하여 그룹핑, SELECT, HAVING, ORDER BY 등 구문에 활용

### 종류
#### 집계 함수 
- 여러 행 또는 테이블 전체 행으로부터 하나의 결과값을 반환하는 함수
```
SELECT 컬럼1, ... 집계함수
FROM 테이블명
[WHERE 조건]
GROUP BY 컬럼1 ...
[HAVING 조건식(집계함수 포함)]
```
#### 그룹 함수 : 소그룹 간의 소계 및 중계 등의 중간 합계 분석 데이터를 산출하는 함수
- 테이블의 전체 행을 하나 이상의 컬럼을 기준으로 컬럼 값에 따라 그룹화하여 그룹별로 결과를 출력하는 함수
- 유형 : ROLLUP, CUBE, GROUPING SETS
- ROLLUP 
  - 소계(소그룹의 합계) 등 중간 집계 값을 산출하기 위한 그룹 함수
  - __지정 컬럼의 수보다 하나 더 큰 레벨__ 만큼의 중간 집계 값 생성
  - 계층별로 구성되므로 __순서가 바뀌면 수행 결과가 바뀜__ 
```
SELECT 컬럼1, ... 집계함수
FROM 테이블명
GROUP BY [컬럼...] ROLLUP 컬럼
```

- CUBE
  - __결합 가능한 모든 값에 대해 다차원 집계를 생성__ 하는 그룹 함수. 연산이 많아 시스템에 부담
```
SELECT 컬럼1, ... 집계함수
FROM 테이블명
GROUP BY [컬럼...] CUBE (컬럼1...)
```

- GROUPING SETS 
  - 집계 대상 컬럼들에 대한 개별 집계 구할 수 있음. 컬럼 간 __순서와 무관한 결과__ 를 얻을 수 있는 그룹 함수
```
SELECT 컬럼1, ... 집계함수
FROM 테이블명
GROUP BY [컬럼...] GROUPING SETS (컬럼1...)
```
#### 윈도 함수 (OLAP)
- 온라인 분석 처리 용도로 사용
- 윈도 함수에는 OVER 문구가 필수

- 분류 : 순위 함수, 행 순서 함수, 그룹 내 비율 함수
- 순위 함수 : 레코드의 순위를 계산하는 함수
  - RANK : __동일 순위의 레코드 존재 시 후순위 넘어감__ (2,2,2,5,6...)
  - DENSE_RANK : __동일 순위의 레코드 존재 시에도 순위 넘어가지 않음__ (2,2,2,3,4...)
  - ROW_NUMBER : 동일 순위 값이 존재해도 __무관하게 연속 번호 부여__ (2,3,4,5,6...)
```
SELECT NAME,
       SALARY,
       RANK() OVER ... ,
       DENSE_RANK() OVER ... ,
       ROW_NUMBER() OVER ... 
```
- 행 순서 함수 : 가장 먼저 나오거나 가장 뒤에 나오는 값, 이전/이후의 값 출력
  - FIRST_VALUE : 파티션별 윈도에서 __가장 먼저 나오는 값__ 을 찾음
  - LAST_VALUE : 파티션별 윈도에서 __가장 늦게 나오는 값__ 을 찾음
  - LAG : 이전 로우의 값 반환
  - LEAD : 이후 로우의 값 반환
```
SELECT NAME,
       SALARY,
       FIRST_VALUE(NAME) OVER ... ,
       LAST_VALUE(NAME) OVER ... ,
       LAG(NAME) OVER ... ,
       LEAD(NAME) OVER ...
```
- 그룹 내 비율 함수 : 백분율, 행 순서별 백분율 등
  - RATIO_TO_REPORT : 각 로우의 상대적 비율 반환
  - PERCENT_RANK : 제일 먼저 나오는 것 0, 제일 늦게 나오는 것 1로 하여 백분율 구하는 함수
```
SELECT NAME,
       SALARY,
       RATIO_TO_REPORT(SALARY) OVER ... ,
       PERCENT_RANK() OVER ... ,
```






















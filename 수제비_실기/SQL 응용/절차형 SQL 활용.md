# 절차형 SQL
- SQL 언어에서도 절차 지향적인 프로그램이 가능하도록 하는 트랜잭션 언어
- 종류 : 프로시저, 사용자 정의함수, 트리거

## 프로시저
- 일련의 쿼리들을 하나의 함수처럼 실행하기 위한 쿼리의 집합
- 구성
  - 선언부 (DECLARE)
  - 시작/종료부 (DEGIN/END)
  - 제어부 (CONTROL)
  - SQL
  - 예외부 (EXCEPTION)
  - 실행부 (TRANSACTION)

## 사용자 정의함수
- 일련의 SQL 처리를 수행하고, 수행 결괄르 단일 값으로 반환할 수 있는 절차형 SQL
- 기본적인 사항은 프로시저와 동일, 반환 부분만 다름
- 구성
  - 선언부 (DECLARE)
  - 시작/종료부 (DEGIN/END)
  - 제어부 (CONTROL)
  - SQL
  - 예외부 (EXCEPTION)
  - 반환부 (TRANSACTION)

## 트리거 [ ★★★ ]
- DBMS에서 삽입, 갱신, 삭제 등의 이벤트가 발생할 때마다 관련 작업이 자동으로 수행되는 절차형 SQL
- 특정 테이블에 대한 데이터 변경을 시작점으로 설정, 그와 관련된 작업을 자동적으로 수행하기 위해 사용
- 종류 : 행 트리거 (데이터 변화마다 실행), 문장 트리거 (단 한번 실행)
- 반환 값이 없고 DML을 주된 목적으로 한다는 점에서 프로시저와 유사함

- 구성
  - 선언부 (DECLARE)
  - 이벤트부 (EVENT)
  - 시작/종료부 (DEGIN/END)
  - 제어부 (CONTROL)
  - SQL
  - 예외부 (EXCEPTION)

- 트리거 문법
```
CREATE [OR REPLACE] TRIGGER 트리거명
[BEFORE | AFTER] 유형 ON 테이블명
[FOR EACH ROW]
BEGIN
END;
```




















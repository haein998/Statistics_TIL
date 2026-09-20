# SQL_ADVANCED 3주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_3rd_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=1YmWy-7-OhQ&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=10
https://www.youtube.com/watch?v=tuQFkzjqEGw&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=11
https://www.youtube.com/watch?v=IOCsreDYqFE&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=12
-->

**교재 실습 예제 파일은 08_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_3rd_TIL

### 4장 SQL 고급 문법
#### 01. MySQL의 데이터 형식
#### 02. 두 테이블을 묶는 조인
#### 03. SQL 프로그래밍 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | 🍽️         |
| 5주차 | p.274~327 | 🍽️         |
| 6주차 | p.330~369 | 🍽️         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. MySQL의 데이터 형식

<!-- MySQL의 데이터 형식에 관해 배우게 된 점을 적어주세요. -->
<!-- 과제 설명 예시처럼 직접 실습 후 사진 한 장 이상을 첨부해주세요. -->

### 데이터 형식       
#### **정수형**         
  소수점이 없는 숫자. 인원 수, 가격, 수량 등에 많이 사용.     
  - TINYINT     
  - SMALLINT     
  - INT       
  - BIGINT      
  인원 수는 INT       
  평균 키는 SMALLINT     
  *UNSIGNED*를 붙이면 0부터 범위가 책정          

#### **문자형**    
  글자를 저장하기 위해 사용     
  - CHAR(개수): 고정길이 문자형. 자릿수가 고정.          
  - VARCHAR(개수): 가변길이 문자형.       
  공간 효율적인 것은 VARCHAR. 내부 성능은 CAHR가 좋음.     

* 데이터가 숫자 형태이라도 연산이나 크기에 의미가 없다면 문자형으로 지정하는 것이 좋음.     
* 전화번호 010을 정수형으로 지정 시 0이 사라져 문자형으로 지정.    

#### 대량의 데이터 형식   
TEXT 형식    
  - TEXT           
  - LONGTEXT        
BLOB 형식: 글자가 아닌 이미지, 동영상 등 데이터           
  - BLOB     
  - LONGBLOB     

#### 실수형       
소수점이 있는 숫자를 저장할 때 사용        
- FLOAT     
- DOUBLE       

#### 날짜형     
날짜 및 시간 저장 시 사용     
- DATE     
- TIME     
- DATETIME     


### 변수의 사용        
SET @변수이름 = 변수의 값 ;  --> 변수의 선언 및 값 대입    
SELECT @변수이름;  --> 변수의 값 출력  

SET @count = 3;       
PREPARE mySQL FROM 'SELECT mem_name, height FROM member ORDER BY height LIMIT ?';      
EXECUTE mySQL USING @count;         

### 데이터 형 변환      
문자형을 정수형으로      
정수형을 문자형으로 바꾸는 것을 형 변환      
- 함수를 이용한 명시적인 변환       
  CAST(값 AS 데이터_형식 [(길이)])      
  CONVERT(값, 데이터_형식 [(길이)])     

- 암시적 변환  
  CONCAT() 함수 사용       

 <img width="1540" height="1154" alt="스크린샷 2026-09-19 165438" src="https://github.com/user-attachments/assets/f69e7768-7c63-4e24-87dc-06a72c762756" />



> **확인문제: 다음 보기에서 데이터 형식의 변환에 사용되는 함수를 2개 고르세요.**

보기는 아래와 같습니다.
```
CONVERT() / DATA() / CAST() / MOVE() / TYPE() / SUM() / AVG() / CURRENT_DATE()
```

```
CONVERT()         
CAST()        

```


## 2. 두 테이블을 묶는 조인

<!-- 두 테이블을 묶는 조인에 관해 배우게 된 점을 적어주세요. -->
<!-- 과제 설명 예시처럼 직접 실습 후 인증 사진 4장 이상을 첨부해주세요. -->

조인: 두 개의 테이블을 묶어 하나의 결과를 만들어 내는 것      

### 내부 조인   

#### 일대다 관계의 이해        
여러 정보를 주제에 따라 분리해서 저장하면서 한 테이블에는 하나의 값만 존재하지 않고 연결된 다른 테이블에는 여러 값이 존재할 수 있는 관계       

#### 내부조인의 기본         
물건 배송을 위해 구매한 회원의 주소 및 연락처를 알아야 하는데 이를 위해 회원 테이블과 구매 테이블을 결합하는 것 => 내부 조인     
WHERE buy.mem_id = 'GRL'  <- 구매 테이블의 7번째에 있는 GRL에 대해서만 결합 진행       

#### 내부 조인의 간결한 표현         
각 열이 어느 테이블에 속한 것인지 명확하게 표현하는 것은 오히려 복잡해보임.    
FROM 절에 나오는 테이블 이름 뒤에 별칭을 줘서 간결하게 표현.     

'''      
SELECT B.mem_id, M.mem_name, B.prod_name, M.addr, CONCAT(m.phone1, M.phone2) '연락처'     
  FROM buy B       
    INNER JOIN member M      
    ON B.mem_id = M.mem_id ;         
'''    


### 외부 조인      

#### 외부 조인의 기본     
외부 조인은 두 테이블을 조인할 때 필요한 내용이 한 쪽 테이블에만 있어도 결과를 추출할 수 있음.      

'''        
SELECT <열 목록>    
FROM <첫 번째 테이블(LEFT 테이블)>      
    <LEFT | RIGHT | FULL> OTHER JOIN <두 번째 테이블(RIGHT 테이블)>     
    ON <조인 될 조건 >     
[WHERE 검색 조건] ;        
'''       

LEFT OUTER JOIN은 왼쪽 테이블의 내용은 모두 출력되어야 한다 의미     

'''   
SELECT M.mem_id, M.mem_name, B.prod_name, M.addr    
  FROM member M       
    LEFT OUTER JOIN buy B         
    ON M.mem_id = B.mem_id        
  ORDER BY M.mem_id;        
'''      

RIGHT OUTER JOIN은 오른쪽 테이블 기준으로       

### 기타 조인        

#### 상호 조인     
한 쪽 테이블의 모든 행과 다른 쪽 테이블의 모든 행을 조인시키는 기능         
상호 조인 결과는 두 테이블의 각 행 수를 곱한 개수     
    특징        
    - ON 구문 사용 불가  
    - 결과 내용은 의미 없음. 랜덤으로 조인하기에      
    - 상호 조인의 주 용도는 테스트를 위해 대용량의 데이터 생성 시    

'''      
SELECT COUNT(*) "데이터 개수"        
  FROM sakila.inventory      
    CROSS JOIN world.city;      
'''        

#### 자체 조인      
자신이 자신과 조인한다는 의미    

'''      
SELECT A.emp "직원", B.emp "직속상관", B.phone "직속상관연락처"    
  FROM emp_table A        
    INNER JOIN emp_table B     
    ON A.manager = B.emp       
  WHERE A.emp = '경리부장' ;      
'''     

<img width="1760" height="840" alt="스크린샷 2026-09-20 004334" src="https://github.com/user-attachments/assets/d1914644-ff2a-4554-8ba6-150ebffde674" />
<img width="1476" height="852" alt="스크린샷 2026-09-20 004215" src="https://github.com/user-attachments/assets/48d399ab-196c-4225-a748-313f4df6a107" />
<img width="1690" height="1116" alt="스크린샷 2026-09-20 004127" src="https://github.com/user-attachments/assets/48e29059-4b9c-41c5-9188-2b3918d0994b" />
<img width="1234" height="1086" alt="스크린샷 2026-09-20 004104" src="https://github.com/user-attachments/assets/838d81fa-6621-4a4a-8182-7801fa1fedb4" />



> **확인문제: 다음 SQL은 회원으로 가입만 하고, 한 번도 구매한 적이 없는 회원의 목록을 조회하는 쿼리입니다. 빈칸에 들어갈 가장 적절한 구문을 고르세요..**

```sql
SELECT DISTINCT M.mem_id, B.prod_name, M.mem_name, M.addr
  FROM member M
    LEFT OUTER JOIN buy B
    ON M.mem_id = B.mem_id
  __________
  ORDER BY M.mem_id;
```
보기는 아래와 같습니다.
```
1. JOIN B.prod_name IS NULL
2. LIMIT B.prod_name IS NULL
3. HAVING B.prod_name IS NULL
4. WHERE B.prod_name IS NULL
```
```
4번      

```

## 3. SQL 프로그래밍 

<!-- IF문, CASE문, WHILE문에 관해 배우게 된 점을 적어주세요. -->

#### 스토어드 프로시저   
MySQL에서 프로그래밍 기능이 필요할 때 사용하는 데이터베이스 개체     

**스토어드 프로시저 구조**        
'''    
DELMITER $$      
CREATE PROCEDURE 스토어드_프로시저_이름()         
BEGIN         
    이 부분 SQL 프로그래밍 코딩    
END $$     
DEELIMITER ;        
CALL 스토어드_프로시저_이름();         
'''        

### IF문     
조건식이 참이라면 SQL 문장들을 실행하고 그렇지 않으면 패스    
'''       
IF <조건식> THEN    
          SQL 문장들       
END IF ;      
'''       

두 문장 이상 처리할 경우 BEGIN ~ END로 묶어줘야 함     

### IF ~ ELSE 문        
조건에 따라 다른 부분을 수행     
조건이 참이라면 1시행. 아니면 2시행.      

'''     
DROP PROCEDURE IF EXISTS ifProc2;    
DELIMITER $$     
CREATE PROCEDURE ifProc2()        
BEGIN     
  DECLATE myNum INT;        
  SET myNum = 200;        
  IF myNum = 100 THEN  
    SELECT '100입니다.' ;        
  ELSE          
    SELECT '100이 아닙니다.' ;       
  END IF;        
END $$     
DELIMITER ;        
CALL ifProc2();       
'''       

### CASE 문     
2가지 이상의 여러 가지 경우 처리 가능. '다중분기'        

'''     
CASE       
  WHEN 조건1 THEN     
    SQL 문장들 1      
  WHEN 조건2 THEN     
    SQL 문장들 2        
  WHEN 조건3 THEN     
    SQL 문장들 3          
  ELSE 
    SQL 문장들 4      
END CASE ;      
'''        

WHEN이 여러개면 조건을 여러 번 반복       

#### CASE 문의 활용       

'''       
SELECT mem_id, SUM(price*amount) "총구매액"      
  FROM buy      
  GROUP BY mem_id;       
'''         

'''    
SELECT M.mem_id, M.mem_name, SUM(price*amount) "총구매액",       
      CASE       
          WHEN (SUM(price*amount) >= 1500) THEN '최우수고객'       
          WHEN (SUM(price*amount) >= 1000) THEN '우수고객'       
          WHEN (SUM(price*amount) >= 1) THEN '일반고객'    
        END "회원등급"        
      FROM buy B     
            RIGHT OUTER JOIN member M       
            ON B.mem_id = M.mem_id           
      GROUP BY M.mem_id        
      ORDER BY SUM(price*amount) DESC ;     
'''      

### WHILE 문       
조건식이 참인 동안 SQL 문장들을 계속 반복      
'''          
WHILE <조건식> DO      
      SQL 문장들      
END WHILE ;      
'''     

### 동적 SQL     
변경되는 내용을 실시간으로 적용시켜 사용할 수 있음       

#### PREPARE와 EXECUTE       
'''      
use market_db ;       
PREPARE myQuery FROM 'SELECT * FROM member WHERE mem_id = "BLK"';        
EXECUTE myQuery;    
DEALLOCATE PREPARE myQuery ;        
'''      

> **확인문제: 다음은 CASE 문의 형식입니다. 빈칸에 들어갈 가장 적절한 명령어를 보기에서 고르세요..**

```sql
CASE
    (1) 조건 THEN
        SQL문장들1
    ELSE
        SQL문장들4
END (2);
```

보기는 아래와 같습니다.
```
WHEN / THEN / CURRENT / DATE / TIME / IF / END IF / CASE
```

```
여기에 답을 적어주세요!
(1) WHEN     
(2) CASE        

```


---

# 2️⃣ 실습과제

## 1. 데이터베이스 구축

아래 코드를 MySQL Workbench에 붙여넣은 후,  
**전체 드래그 → 실행 (Ctrl + shift + Enter)** 하여 데이터베이스를 구축하세요.

```sql
-- 1. 데이터베이스 생성
CREATE DATABASE IF NOT EXISTS week3_db;

-- 2. 사용할 데이터베이스 선택
USE week3_db;

-- 3. 기존 테이블 삭제 (초기화용)
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS customers;

-- 4. 테이블 생성 (조인 실습용)
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(20),
    signup_date_str VARCHAR(8) 
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,           
    order_date_str VARCHAR(8), 
    amount_str VARCHAR(10)     
);

-- 5. 데이터 삽입
INSERT INTO customers VALUES
(1, '신영', '20241528'),
(2, '경모', '20220261'),
(3, '세원', '20203401'),
(4, '진우', '20221024'),
(5, '성환', '20225100'),
(6, '혜준', '20244946'),
(7, '채은', '20250412'),
(8, '다나', '20212774'); -- 주문 없는 고객(외부 조인용)

INSERT INTO orders VALUES
(101, 1, '20240220', '12000'),
(102, 1, '20240303', '30000'),
(103, 2, '20240111', '15000'),
(104, 3, '20221201', '9000'),
(105, 5, '20231111', '20000'),
(106, 7, '20220707', '5000'),
(107, 99, '20240210', '7000'); -- 고객 테이블에 없는 customer_id (외부 조인용)
```

## 2. 실습 문제

다음 SQL 문을 작성하고 실행 결과를 확인 후 인증 사진을 아래에 업로드하세요.

1. **데이터 형식 변환**
   - orders 테이블의 `order_date_str`을 DATE 형식으로 변환하여 조회하시오.
   (힌트: STR_TO_DATE 사용)

2. **데이터 형식 변환**
   - orders 테이블의 `amount_str`을 숫자형으로 변환하여 조회하시오.

3. **내부 조인 (INNER JOIN)**
   - customers와 orders를 customer_id 기준으로 내부 조인하여
     고객 이름(name)과 주문 번호(order_id)를 함께 조회하시오.

4. **외부 조인 (LEFT JOIN)**
   - customers를 기준으로 LEFT JOIN을 수행하여,
     주문이 없는 고객도 함께 조회하시오.

5. **스토어드 프로시저 (IF문 사용)**
   - 입력받은 금액이 10000 이상이면 '고액 주문',
     그렇지 않으면 '일반 주문'을 출력하는
     프로시저를 생성하시오.
   - 생성 후 CALL로 실행 결과를 확인하시오.


<img width="1378" height="698" alt="스크린샷 2026-09-20 142521" src="https://github.com/user-attachments/assets/2863d67c-3bd6-4e06-bd18-f6118e65f2e7" />
<img width="1192" height="670" alt="스크린샷 2026-09-20 142608" src="https://github.com/user-attachments/assets/78bebf3b-908a-4df8-aeeb-69d7628f4e16" />
<img width="1062" height="802" alt="스크린샷 2026-09-20 142825" src="https://github.com/user-attachments/assets/ee3efa78-0fcf-4d1e-ad7a-494ea846a60d" />
<img width="1104" height="840" alt="스크린샷 2026-09-20 142846" src="https://github.com/user-attachments/assets/34073464-185e-4ad7-8b42-961fb598fcc6" />
<img width="1310" height="972" alt="스크린샷 2026-09-20 153223" src="https://github.com/user-attachments/assets/adb0732e-3420-4dd8-80e3-1f17c7864f08" />



### 🎉 수고하셨습니다.







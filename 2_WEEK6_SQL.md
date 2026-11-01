# SQL_ADVANCED 6주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_6th_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=cw1wGN0ZdFA&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=19
https://www.youtube.com/watch?v=bMQ_dAoaMzA&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=20
https://www.youtube.com/watch?v=bggWVsBmKag&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=21
-->

**교재 실습 예제 파일은 08_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_6th_TIL

### 7장 스토어드 프로시저
#### 01. 스토어드 프로시저 사용 방법
#### 02. 스토어드 함수와 커서
#### 03. 자동 실행되는 트리거 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | ✅         |
| 5주차 | p.274~327 | ✅         |
| 6주차 | p.330~369 | ✅         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. 스토어드 프로시저 사용 방법 


SQL: 데이터베이스에서 사용되는 언어    
MySQL의 스토어드 프로시저는 SQL에 프로그래밍 기능 추가해서 일반 프로그래밍 언어와 비슷한 효과    

### 스토어드 프로시저    
스토어드 프로시저: MySQL에서 제공하는 프로그래밍 기능.   
                  쿼리문의 집합으로 볼 수 있으며, 어떤 동작을 일괄 처리하기 위한 용도로도 사용    

```
DELIMITER $$      
CREATE PROCEDURE 스토어드_프로시저_이름(IN 또는 OUT 매개변수)   
BEGIN   

    이 부분에 SQL 프로그래밍 코드 작성    
END $$   
DELIMITER ;   
```   

DELIMITER: '구분자'라는 의미.   

#### 스토어드 프로시저 호출하는 형식    
CALL 스토어드_프로시저_이름();     

#### 스토어드 프로시저의 생성    
```   
USE market_db;       
DROP PROCEDURE IF EXISTS user_proc;   
DELIMITER $$     
CREATE PROCEDURE user_proc()     
BEGIN     
    SELECT * FROM member;     
END $$    
DELIMITER ;        

CALL user_proc();       
```       

#### 스토어드 프로시저의 삭제    
DROP PROCEDURE    

#### 매개변수 사용      
IN 입력_매개변수_이름 데이터_형식       
CALL 프로시저_이름(전달_값);    

OUT 출력_매개변수_이름 데이터_형식   
CALL 프로시저_이름(@변수명);    
SELECT @변수명;    

#### 입력 매개변수 스토어드 프로시저 생성하고 실행   

```     
USE market_db;     
DROP PROCEDURE IF EXISTS user_proc1;      
DELIMITER $$    
CREATE PROCEDURE user_proc1(IN useName VARCHAR(10))     
BEGIN      
 SELECT * FROM member WHERE mem_name = userName;   
END $$   
DELIMITER;     

CALL user_proc1('에이핑크');     
```    

#### 입력 매개변수의 활용   
```    
USE market_db;    
DROP PROCEDURE IF EXISTS user_proc1;   
DELIMITER $$   
CREATE PROCEDURE user_proc1(IN useName VARCHAR(10))     
BEGIN    
 SELECT * FROM member WHERE mem_name = userName;     
END $$    
DELIMITER ;      

CALL user_proc1('에이핑크');    
```    

#### SQL 프로그래밍의 활용    

```    
DROP PROCEDURE IF EXISTS ifelse_proc;     
DELIMITER $$    
CREATE PROCEDURE ifelse_proc(       
    IN memName VARCHAR(10)   
)       
BEGIN       
    DECLARE debutYear INT; -- 변수 선언      
    SELECT YEAR(debut_date) into debutYear FROM member    
        WHERE mem_name = memName;       
    IF (debutYear >= 2015) THEN     
            SELECT '신인 가수네요. 화이팅 하세요.' AS '메세지';    
    ELSE    
            SELECT '고참 가수네요. 그동안 수고하셨어요.' AS '메세지';   
    END IF;    
END $$    
DELIMITER ;      

CALL ifelse_proc('오마이걸');     

```    



<!-- 이번 챕터에서는 확인문제를 실습 인증으로 대체하여 진행합니다. 제시된 실습을 흐름에 맞게 진행한 후, 실습 과정이 보일 수 있도록 인증 사진을 2장 이상 제출해 주세요. -->

<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->


## 2. 스토어드 함수와 커서 

스토어드 함수: MySQL에서 제공하는 내장 함수 외에 직접 함수를 만드는 기능 제공    
직접 스토어드 함수 작성해서 사용 가능  
스토어드 함수와 스토어드 프로시저는 모양 비슷. but 세부적으로 다름      

### 스토어드 함수       
직접 만들어서 사용하는 함수를 스토어드 함수    

```    
DELIMITER $$     
CREATE FUNCTION 스토어드_힘수_이름(매개변수)    
    RETURNS 반환형식      
BEGIN    

    이 부분에 프로그래밍 코딩    
    RETURN 반환값;      

END $$  
DELIMITER ;    
SELECT 스토어드_힘수_이름();     

```   

** 스토어드 함수와 스토어드 프로시저의 차이점 **       
- 스토어드 함수는 ***RETURNS문***으로 반환할 값의 데이터 형식 저장   
- 스토어드 함수의 매개변수는 모드 ***입력 매개변수***. IN을 붙이지 않음   
- 스토어드 함수는 ***SELECT문*** 안에서 호출    
  스토어드 프로시저는 CALL로 호출    
- 스토어드 함수 안에서 SELECT 사용 불가    
  스토어드 프로시저 안에서는 SELECT 문 사용 가능   

### 커서로 한 행씩 처리하기       

**커서**: 테이블에서 한 행씩 처리하기 위한 방식     
첫 번째 행을 처리한 후 마지막 행까지 한 행씩 접근해서 값을 처리   
처음에는 커서가 행의 시작을 가리킨 후 한 행씩 차례대로 접근    

```    
SELECT calcYearFunc(2007) INTO @debut2007;   
SELECT calcYearFunc(2013) INTO @debut2013;    
SELECT @debut2007-@debut2013 AS '2007과 2013 차이';   
```    

#### 데뷔 연도 입력하면, 활동 기간이 얼마나 되었는지 출력해주는 함수   
```    
DROP FUNCTION IF EXISTS calYearFunc;   
DELIMITER $$   
CREATE FUNCTION calcYearFunc(dYear INT)   
    RETURNS INT   
BEGIN   
    DECLARE runYear INT; -- 활동기간(연도)   
    SET runYear = YEAR(CURDATE()) - dYEAR;   
    RETURN runYear;   
END $$   
DELIMITER ;   
```   

------- 
데뷔 연도가 매개변수    
현재 연도 - 데뷔 연도 계산하여 활동한 햇수 계산    
계산 결과 반환   
---------

#### 스토어드 함수의 사용    
스토어드 함수 생성 권한 허용 필요   
```    
SET GLOBAL log_bin_trust_function_creators = 1;    
```   

#### 커서의 단계별 실습   
1. 사용할 변수 준비    
2. 커서 선언하기   
3. 반복 조건 선언하기   
4. 커서 열기   
5. 행 반복하기    
6. 커서 닫기   

LEAVE: 반복할 이름 빠져나감. 
FETCH: 한 행씩 읽어오는 것.   

```   
USE market_db;   
DROP PROCEDURE IF EXISTS cursor_proc;   
DELIMITER $$   
CREATE PROCEDURE cursor_proc()    
BEGIN   
    DECLARE memNumber INT;    
    DECLARE cnt INT DEFAULT 0;   
    DECLARE totNumber INT DEFAULT 0;   
    DECLARE end0fRow BOOLEAN DEFAULT FALSE;    

    DECLARE memberCursor CURSOR FOR   
        SELECT mem_number FROM member;   

    DECLARE CONTINUE HANDLER   
        FOR NOT FOUND SET end0fRow = TRUE;   

    OPEN memberCursor;    

    cursor_loop: LOOP   
        FETCH memberCursor INTO memNumber;   

        IF end0fRow THEN   
            LEAVE cursor_loop;    
        END IF;   

        SET cnt = cnt + 1;   
        SET totNumber = totNumber + memNumber;   
    END LOOP cursor_loop;   

    SELECT (totNumber/cnt) AS '회원의 평균 인원 수';   

    CLOSE memberCursor;    

END $$   
DELIMITER ;    
```    

```   
CALL cursor_proc();    
```   




<!-- 이번 챕터에서는 확인문제를 실습 인증으로 대체하여 진행합니다. 제시된 실습을 흐름에 맞게 진행한 후, 실습 과정이 보일 수 있도록 인증 사진을 2장 이상 제출해 주세요. -->

<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->


## 3. 자동 실행되는 트리거 

트리거: 자동으로 수행하여 사용자가 추가 작업을 잊어버리는 실수를 방지    
데이터의 무결성: 데이터 오류 발생 방지   

### 트리거    
INSERT나 UPDATE 또는 DELETE 작업이 발생하면 실행되는 코드   

#### 트리거의 기본 작동      
트리거는 테이블에서 **DML**문 (INSERT, UPDATE, DELETE)의 이벤트가 발생할 때 작동    

```    
USE market_db;   
CREATE TABLE IF NOT EXISTS trigger_table (id INT, txt VARCHAR(10));      
INSERT INTO trigger_table VALUES(1, '레드벨벳');     
INSERT INTO trigger_table VALUES(2, '잇지');     
INSERT INTO trigger_table VALUES(3, '블랙핑크');     
```       

```     
DROP TRIGGER IF EXISTS myTrigger;       
DELIMITER $$       
CREATE TRIGGER myTrigger       
    AFTER DELETE     
    ON trigger_table       
    FOR EACH ROW       
BEGIN    
    SET @msg = '가수 그룹이 삭제됨'; --트리거 실행 시 작동되는 코드들     
END $$      
DELIMITER ;        
```         

```     
SET @msg = '';      
INSERT INTO trigger_table VALUES(4, '마마무');     
SELECT @msg;      
UPDATE trigger_table SET txt = '블핑' WHERE id = 3;      
SELECT @msg;       
```       

```     
DELETE FROM trigger_table WHERE id = 4;      
SELECT @msg;      
```       

### 트리거 활용      
테이블에 입력/수정/삭제되는 정보를 백업하는 용도로 활용 가능    

INSERT, UPDATE, DELETE 작업이 수행되면 임시로 사용되는 시스템 테이블이 2개 있음    
**NEW, OLD**    

**NEW 테이블** 
INSERT(새 값) 형태로 테이블에 들어가기 전 NEW 테이블에 잠깐 들어간 후, 테이블에 새 값으로 들어감      

**OLD 테이블**        
DELETE(예전 값) 형태로 삭제되기 전 OLD 테이블에 잠깐 들어감    
그래서 AFTER DELETE 트리거를 만들어도 삭제된 후 OLD.열 이름 형식으로 예전 값에 접근 가능    

UPDATE(새 값, 예전 값)을 사용하면 NEW테이블과 OLD 테이블 모두 사용    


<!-- 이번 챕터에서는 확인문제를 실습 인증으로 대체하여 진행합니다. 제시된 실습을 흐름에 맞게 진행한 후, 실습 과정이 보일 수 있도록 인증 사진을 2장 이상 제출해 주세요. -->

<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->


---


### 🎉 수고하셨습니다.







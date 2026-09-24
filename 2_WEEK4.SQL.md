# SQL_ADVANCED 4주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_4th_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=DMNpkj_bZIs&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=13
https://www.youtube.com/watch?v=BUHj-behLyc&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=14
https://www.youtube.com/watch?v=JrXWxku7ZIM&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=15
-->

**교재 실습 예제 파일은 08_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_4th_TIL

### 5장 테이블과 뷰
#### 01. 테이블 만들기
#### 02. 제약조건으로 테이블을 견고하게
#### 03. SQL 가상의 테이블: 뷰 


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | ✅         |
| 4주차 | p.216~271 | ✅         |
| 5주차 | p.274~327 | 🍽️         |
| 6주차 | p.330~369 | 🍽️         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. 테이블 만들기 

### 테이블    
표 형태로 구성된 2차원 구조.         
행(로우 row, 레코드 record) 열(컬럼 column, 필드 field)로 구성    

회원 테이블에서는 아이디는 기본 키로 지정. 평균 키는 TINYINT UNSIGGNED를 사용해서 0~255 범위로 지정   
구매 테이블에서는 아이디는 외래 키로 설정 <- 구매테이블의 아이디와 회원 테이블의 아이디를 연결      

### GUI 환경에서 테이블 만들기  

#### 데이터 베이스 생성하기 
1. MySQL Workbench를 실행해서 'root/000'으로 접속한 후 새 쿼리 창 생성. 번개 아이콘 누르기   
2. SQL로 만든 데이터베이스는 화면에 바로 적용되지 않기 때문에 SCHEMAS 패널에 보이지 않음. 그래서 SCHMAS 패널의 빈 곳에서 마우스 오른쪽 버튼을 클릭하고 Refresh All을 선택      

#### 테이블 생성하기 
1. 데이터 베이스를 확장해서 Tables를 선택하고 마우스 오른쪽 버튼을 클리한 후 Create Table을 선택함.        
2. 앞에서 설계한 대로 회원 테이블 평균 키는 height의 Datatype을 TINYINT로 설정하고 UN을 체크.   
3. Apply SQL script to Database 창에서 생성된 CREATE TABLE 코드를 확인. 쿼리 창 종료     
4. 같은 방식으로 구매 테이블 생성. 순번은 **자동 증가(AUTO_INCREMENT)** 를 위해 AI로 지정. 가격과 수량은 음수가 들어가지 않아 UN 처리    
5. GUI에서는 기본 키-외래 키 관계를 약간 수정.         
6. 생성된 외래 키는 SCHEMAS 패널에서 확인 가능      

#### 데이터 입력하기     
1. SCHEMAS 패널에서 [naver_db] - [Tables] - [member]를 선택하고 마우스 오른쪽 버튼을 눌러 [Select Rows - Limit 1000] 선택    
2. SELECT 문이 자동 생성되고 [Result Grid] 창에 결과 보임     
3. Insert new row 아이콘 클릭하고 값을 3개 행만 입력    
4. [SCHEMAS] 패널의 [buy]에서 [Select Rows - Limit 1000] 선택. Insert new row 아이콘 클릭하고 행 3개 입력    
5. 오류 발생 -> 회원 테이블과 구매 테이블은 기본 키 - 외래 키로 연결 -> 이는 구매 테이블의 mem_id 값은 반드시 회원 테이블의 mem_id로 존재해야 한다는 의미. -> 스크립트 창 먼저 종료   
6. 행 삭제를 위해 [Result Grid] 창에서 APN앞 빈 부분 선택하고 [Delete Rows] 선택      
7. 창에서 어플라이 하고 쿼리 창 종료 [File] - [Close Tab]    

### SQL로 테이블 만들기      

CREATE TABLE sample_table (num INT);        
데이터 베이스와 회원 테이블을 생성하고 데이터를 입력      

#### 데이터베이스 생성하기    
새 쿼리 창 준비.       
```      
DROP DATABASE IF EXISTS naver_db;       
CREATE DATABASE naver_db;         
```    
앞에 사용한 naver_db 삭제 후 다시 생성       
[Schemas] 패널의 빈 곳에서 마우스 오른쪽 버튼 [Refresh All]        

#### 테이블 생성하기     
1. CREATE TABLE 구문으로 회원 테이블 생성      
```          
USE naver_db;    
DROP TABLE IF EXITS member;        
CREATE TABLE member -- 회원 테이블      
( mem_id        CHAR(8), -- 회원 아이디(PK)
  mem_name      VARCHAR(10), -- 이름    
  mem_number    TINYINT, -- 인원수    
  addr          CHAR(2), -- 주소(경기, 서울, 경남 식으로 2글자만 입력)     
  phone1        CHAR(3), -- 연락처의 국번(02, 031, 055 등)     
  phone2        CHAR(8), -- 연락처의 나머지 전화번호(하이픈 제외)     
  height        TINYINT UNSIGNED, -- 평균 키       
  debut_date    DATE -- 데뷔 일자     
  );      
```       
2. NULL 및 NOT NULL을 지정해서 테이블을 다시 생성. 아무 것도 지정하지 않으면 기본값으로 NULL을 허용.    
3. 테이블 기본 키 설정. 기본 키로 설정하기 위해서는 지정할 열 뒤에 PRIMARY KEY 문을 붙여주면 됨. 기본 키로 지정된 열에는 NOT NULL을 생략해도 당연히 NOT NULL로 취급   
```    
DROP TABLE IF EXITS member;        
CREATE TABLE member     
( mem_id        CHAR(8) NOT NULL PRIMARY KEY, 
  mem_name      VARCHAR(10) NOT NULL,     
  mem_number    TINYINT NOT NULL,   
  addr          CHAR(2) NOT NULL,      
  phone1        CHAR(3) NOT NULL,      
  phone2        CHAR(8) NOT NULL, 
  height        TINYINT UNSIGNED NULL,       
  debut_date    DATE NULL     
  );    
```    

4. 열 이름과 테이블 형식을 먼저 지정한 후 나머지 조건을 정하기. 테이블 생성 후 [Schemas]패널에서 [naver_db] - [Tabels]를 마우스 오른쪽 버튼으로 클릭하고 [Refresh All]을 선택하여 생성한 테이블 확인   
5. 구매 테이블을 만드는 경우. AUTO_INCREMENT로 지정한 열은 PRIMARY KEY나 UNIQUE로 꼭 지정     
6. 구매 테이블의 아이디 열을 회원 테이블 아이디 열의 외래 키로 설정하려면 마지막 열의 뒤에 콤마 입력 후 외래 키 관련 문장 입력.    
*FOREIGN KEY(mem_id) REFERENCES member(mem_id)* : 이 테이블의 mem_id 열을 member 테이블의 mem_id 열과 외래 키 관계로 연결해라 뜻       



## 2. 제약조건으로 테이블을 견고하게 

테이블 만들 때 테이블의 구조에 필요한 제약조건 설정  
- 기본 키와 외래 키    
  기본 키는 학번, 아이디, 사번 등 고유 번호 의미하는 열     
  외래 키는 기본 키와 연결되는 열에 지정
- 고유 키          
  이메일, 휴대폰 같이 중복되지 않는 열에는 *고유 키* 지정 가능    
- 체크      
  실수로 입력하는 것을 방지하기 위한 제약 조건  
- 기본값    
  매번 입력하기 귀찮은 경우 제약 조건    
- NOT NULL       
  값을 꼭 입력해야 하는 경우 제약 조건      

제약조건: 데이터의 무결성을 지키기 위해 제한하는 조건.      
데이터 무결성: 데이터에 결함이 없는 상태   

    
### MySQL에서 제공하는 대표적 제약조건    
- PRIMARY KEY 제약조건    
- FOREIGN KEY 제약조건       
- UNIQUE 제약조건     
- CHECK 제약조건      
- DEFAULT 정의      
- NULL 값 허용  


### 기본 키 Primary Key     
데이터를 구분할 수 있는 식별자.    
테이블의 아이디, 학생 테이블의 학번, 직원 테이블의 사번 등 해당       
기본 키의 조건은 중복되지 않고, NULL 값 입력 불가     
대부분의 테이블은 기본 키를 가져야 함.    
기본 키를 설정해야 중복된 데이터가 입력되지 않음.       

#### CREATE TABLE에서 설정하는 기본 키 제약 조건   

방법 1. 
```      
mem_id CHAR(8) NOT NULL PRIMAEY KEY     
```      
방법 2.    
```   
PRIMARY KEY (mem_id)      <- 제일 마지막 행에 추가
```     

#### ALTER TABLE에서 설정하는 기본 키 제약조건    
```     
ALTER TABLE member     
     ADD CONSTRAINT    
     PRIMARY KEY (mem_id);     
```      

### 외래 키 Foreign Key     
외래 키 제약조건은 두 테이블 사이 관계를 연결해주고, 그 결과 데이터의 무결성을 보장해주는 역할      
외래 키가 설정된 열은 꼭 다른 테이블의 기본 키와 연결     
---------------------------------        
기본 키가 있는 회원 테이블은 - 기준 테이블    
외래 키가 있는 구매 테이블은 - 참조 테이블    
구매 테이블의 아이디(FK)는 반드시 회원 테이블의 아이디(PK)로 존재     

* 참조 테이블이 참조하는 기준 테이블의 열은 반드시 기본 키나 고유 키로 설정되어 있어야 함.     

#### CREATE TABLE에서 설정하는 외래 키 제약 조건    
```      
FOREIGN KEY(mem_id) REFERENCES member(mem_id)   
```      
외래 키의 형식: FOREIGN KEY(열 이름) REFERENCES 기준테이블(열 이름)      

#### ALTER TABLE에서 설정하는 외래 키 제약 조건     
```      
ALTER TABLE buy   
    ADD CONSTRAINT     
    FOREIGN KEY (mem_id)    
    REFERENCES member(mem_id);       
```        

#### 기준 테이블의 열이 변경될 경우      
```     
DROP TABLE EXISTS buy;    
CREATE TABLE buy     
( num INT     AUTO_INCREMENT NOT NULL PRIMARY KEY,     
  mem_id      CHAR(8) NOT NULL,        
  prod_name   CHAR(6) NOT NULL   
);      
ALTER TABLE buy        
    ADD CONSTRAINT     
    FOREIGN KEY(mem_id) REFERENCES member (mem_id)     
    ON UPDATE CASCADE     
    ON DELETE CASCADE;     
```    





> **확인문제: 다음 보기 중에서 각 문항이 설명하는 것을 고르세요.**

보기는 아래와 같습니다.
```
CHECK / DEFAULT / PRIMAY KEY / UNIQUE / NOT NULL / FOREIGN KEY
```

```
여기에 답과 그 이유를 적어주세요!
1. 입력되는 데이터가 조건에 맞는지 검사하는 기능: CHECK
2. 값을 입력하지 않으면 자동으로 들어갈 값: DEFAULT 
3. 빈 값을 입력하는 것을 허용하지 않음: NOT NULL 
```


## 3. 가상의 테이블: 뷰 

뷰: 데이터베이스 개체 중 하나. 테이블처럼 데이터를 가지고 있지는 않으나, SELECT 문으로 만들어져 있기에 뷰에 접근하는 순간 SELECT가 실행되고 결과가 화면에 출력    

#### 뷰의 기본 생성      
```     
USE market_db;     
CREATE VIEW v_member   
AS      
        SELECT mem_id, mem_name, addr FROM member;    
```     

#### 뷰의 작동      
뷰는 기본적으로 읽기 전용으로 사용되지만 뷰를 통해 원본 데이터를 수정할 수도 있음.    

#### 뷰를 사용하는 이유   
- 보안에 도움    
- 복잡한 SQL을 단순하게      

#### 뷰의 실제 생성, 수정, 삭제 
뷰에 사용될 열 이름을 테이블과 다르게 지정 가능. 기존 별칭 사용. 중간 띄어쓰기 사용 가능.     
별칭은 열 이름 뒤에 작은 따옴표 또는 큰 따옴표로 묵어주고 형식상 AS 붙여줌.   
뷰를 조회할 때는 백틱 `으로 묶어줘야 함    

뷰의 수정은 ALTER VIEW 구문 사용.     
뷰의 삭제는 DROP VIEW 사용.     
뷰의 정보확인은 DESCRIBE 사용.      
뷰의 소스 코드 확인은 SHOW CREATE VIEW 사용.       
뷰에 설정된 범위 내에서 입력 WITH CHECK OPTION 사용.      
뷰가 참조하는 테이블이 없어서 발생하는 오류 확인은 CHECK TABLE 사용.    



> **확인문제: 다음은 뷰의 특징입니다. 거리가 먼 것을 하나 고르세요.**

보기는 아래와 같습니다.
```
1️⃣ 뷰에는 테이블의 모든 열을 포함시켜야 합니다.
2️⃣ 뷰는 복잡한 SQL을 단순하게 만드는 효과가 있습니다.
3️⃣ 뷰는 보안에 도움이 됩니다.
4️⃣ 일부 사용자가 테이블에는 접근하지 못하게 하고, 뷰에만 접근하도록 설정할 수 있습니다.
```

```
1번  
모든 열 포함할 필요 없음.     
간단하게 만들 수 있음.    

```


---

# 2️⃣ 실습과제

## 1. 데이터베이스 구축

아래 코드를 MySQL Workbench에 붙여넣은 후,  
**전체 드래그 → 실행 (Ctrl + Shift + Enter)** 하여 데이터베이스를 생성하세요.

```sql
CREATE DATABASE IF NOT EXISTS week4_db;
USE week4_db;
```

## 2. 실습문제

1. 다음 조건을 만족하는 `users` 테이블을 생성하시오.
```
- user_id는 INT이며 **기본키(Primary Key)**로 설정합니다.
- name은 VARCHAR(20)이며 NULL을 허용하지 않습니다.
- email은 VARCHAR(50)이며 중복을 허용하지 않습니다.
- signup_date는 DATE 타입으로 설정합니다.
- grade는 INT이며 기본값(Default)을 1로 설정합니다.
```

2. 다음 조건을 만족하는 `orders` 테이블을 생성하시오.
```
- order_id는 INT이며 기본키(Primary Key)로 설정합니다.
- user_id는 INT이며 NULL을 허용하지 않습니다.
- amount는 INT이며 0보다 커야 합니다.
- order_date는 DATE 타입으로 설정합니다.
```

3. 다음 조건을 만족하여 데이터를 삽입하시오.
```
- users 테이블에 3명 이상의 데이터를 직접 INSERT 하시오. (단, user 중 본인이 포함돼야 함)
- orders 테이블에 3건 이상의 데이터를 직접 INSERT 하시오.
```

4. users와 orders 테이블을 활용하여 다음 컬럼을 보여주는 뷰 user_order_view를 생성하시오.
```
- user_id
- name
- amount
```

5. 생성한 user_order_view를 조회하시오.

## 3. 제출 방법

1. 각 문제의 실행 결과가 보이도록 화면을 캡처합니다.
2. 테이블 생성 결과, 데이터 삽입 결과, 뷰 생성 및 조회 결과가 모두 보이도록 제출합니다.

<!-- 이 부분을 지우고 인증사진을 제출해주세요.-->

### 🎉 수고하셨습니다.







# SQL_ADVANCED 2주차 정규 과제 

📌SQL_ADVANCED 정규과제는 매주 정해진 분량의 『*혼자 공부하는 SQL*』 을 읽고 학습하는 것입니다. 이번주는 아래의 **SQL_ADVANCED_2nd_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=_JURyg_KzHE&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=7
https://www.youtube.com/watch?v=6qkPy7RfLqQ&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=8
https://www.youtube.com/watch?v=WWAFAm9op2U&list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm&index=9
-->

**교재 실습 예제 파일은 08_SQL_ADVANCED_Template 레포지토리의 src 폴더에 업로드되어 있습니다. market_db 파일도 해당 폴더에 함께 포함되어 있으니 참고하시기 바랍니다.**

**👀(수행 인증샷은 필수입니다.)** 

## SQL_ADVANCED_2nd_TIL

### 3장 SQL 기본 문법
#### 01. 기본 중에 기본 SELECT ~ FROM ~ WHERE
#### 02. 좀 더 깊게 알아보는 SELECT문
#### 03. 데이터 변경을 위한 SQL문


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~99    | ✅         |
| 2주차 | p.102~155   | ✅         |
| 3주차 | p.158~213  | 🍽️         |
| 4주차 | p.216~271 | 🍽️         |
| 5주차 | p.274~327 | 🍽️         |
| 6주차 | p.330~369 | 🍽️         |
| 7주차 | p.372~407 | 🍽️         |


<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 학습 내용 정리

## 1. 기본 중에 기본 SELECT ~ FROM ~ WHERE

### SELCET문: 
구축이 완료된 테이블에서 데이터를 추출하는 기능        
기본 형식 SELCET (열이름) ~ FROM (테이블 이름) ~ WHERE (조건식)          

### USE 문: 
market_db 데이터베이스를 선택하는 문장 

USE 데이터베이스_이름;        
SELECT 문을 실행하려면 먼저 사용할 데이터 베이스 지정      
지금부터 이 DB를 사용하겠다는 의미       

### SELECT문의 기본 형식       
```         
SELECT 열_이름   
    FROM 테이블_이름         
    WHERE 조건식       
    GROUP BY 열_이름     
    HAVING 조건식       
    ORDER BY 열_이름      
    LIMIT 숫자        
```        

### USE market db;     
.
.
.

### SELECT * FROM member;      
---> SELCET: 테이블에서 데이터를 가져올 때 사용하는 예약어      
    *: 일반적으로 '모든 것'을 의미. 현재 코딩에서는 모든 열을 말함   
    FROM: 테이블이름에서 내용을 가져온다는 의미   
    member: 조회할 테이블 이름       
===> member 테이블에서 모든 열의 내용을 가져와라.         

### SELCET * FROM market_db.member;  
### SELECT * FROM member;          
테이블 전체 이름은 "" 데이터베이스_이름.테이블_이름"" 형식

### SELECT mem_name FROM member;     
해당 테이블에서 필요한 열만 가져오기     

### SELECT addr, debut_date, mem_name FROM member;     
여러 개의 열을 가져올 땐 콤마로 구분        

## 특정한 조건만 조회하기: SELECT ~ FROM ~ WHERE    
             
             
### WHERE 없이 조회하기      
WHERE 없이 SELECT ~ FROM만으로 테이블 조회 시 모든 행 출력       
               
               
#### 기본적인 WHERE 절      
SELECT 열_이름 FROM 테이블_이름 WHERE 조건식;        
또는       
SELECT 열_이름      
    FROM 테이블_이름         
    WHERE 조건식;     


### 관계 연산자, 논리 연산자의 사용      

```       
SELECT mem_id, mem_name     
    FROM member       
    WHERE height <= 162;      
```         

```       
SELECT mem_name, height     
    FROM member       
    WHERE height >= 163 AND height <= 165;     
```    

혹은      
```       
SELECT mem_name, height  
    FROM member       
    WHERE height BETWEEN 163 AND 165;   
```         
 ** 숫자 범위 사용 시 용이**           

<img width="1544" height="1186" alt="스크린샷 2026-09-13 001940" src="https://github.com/user-attachments/assets/e32334b1-1525-4ef3-b33f-7057dbccce78" />
<img width="1482" height="1028" alt="스크린샷 2026-09-13 002208" src="https://github.com/user-attachments/assets/9de11702-04bf-43db-a347-f6124d427c9c" />




> **확인문제: 주소의 지역이 서울, 경기인 회원을 추출하는 SQL 문입니다. 빈칸에 들어갈 수 있는 것을 모두 고르세요.**

```sql
SELECT *
FROM table
WHERE ________;
```

보기는 아래와 같습니다.
```
1. addr IN('서울', '경기')
2. addr BETWEEN '서울' AND '경기'
3. addr = '서울' OR addr = '경기'
4. addr = '서울' AND addr = '경기'
```

```
1, 3번     
둘 중 하나에 해당하는 주소를 택하도록 코드화된 경우를 선택.     
2번의 BETWEEN은 숫자 범위 사용 시    
4번의 AND는 둘 다 해당하는 경우를 출력하는 경우에 사용     

```


## 2. 좀 더 깊게 알아보는 SELECT문

<!-- ORDER BY절과 GROUP BY절 그리고 HAVING절에 관해 배우게 된 점을 적어주세요. -->


여기에 배우게 된 점을 적어주세요!
### ORDER BY절:      
결과 값이나 개수에 대해서는 영향을 미치지 않지만, 결과가 출력되는 순서를 조절   

```
SELECT mem_id, mem_name, debut_date    
    FROM member    
    ORDER BY debit_date;      
```     
제일 뒤에 **ASC** 를 붙이면 오름차순. **DESC**를 붙이면 내림차순.       
           
ORDER BY 절은 ***WHERE 절 다음***에 나와야 한다.     
```    
SELECT mem_id, mem_name, debut_date, height          
    FROM member     
    WHERE height >= 164     
    ORDER BY height DESC;      
```    


정렬 기준은 1개의 열이 아닌 ***여러 개 열***로 지정 가능.      
첫 번째 지정 열로 정렬 후, 동일할 경우 다음 지정 열로 정렬 가능   
```      
SELECT mem_id, mem_name, debut_date, height   
    FROM member     
    WHERE height >= 164 
    ORDER BY height DESC, debut_Date ASC;      
```       
      
**LIMIT**은 출력하는 개수를 제한     
***LIMIT 시작, 개수 형식***으로 사용. LIMIT 3은 0번째부터 3건이라는 의미     
```  
SELECT *        
    FROM member        
    LIMIT 3;       
```           

**DISTINCT**은 조회된 결과에서 중복된 데이터를 1개만 남김.    
```      
SELECT DISTINCT addr FROM member;    
```    

### GROUP BY절: 
그룹을 묶어주는 역할      

#### 집계함수   
- SUM(): 합계    
- AVG(): 평균   
- MIN(): 최소값      
- MAX(): 최대값     
- COUNT(): 행의 개수     
- COUNT(DISTINCT): 행의 개수 (중복은 1개만 인정)       


HAVING절: WHERE과 비슷한 개념으로 조건을 제한. 집계 함ㅅ웨 대해 조건을 제한하는 것.       
HAVING절은 꼭 GROUP BY 절 다음에 나와야 함.      

```       
SELECT mem_id "회원 아이디", SUM(price*amount) "총 구매 금액"      
    FROM buy      
    GROUP BY mem_id     
    HAVING SUM(price*amount) > 1000      
    ORDER BY SUM(price*amount) DESC; #내림차순, 총 구매액이 큰 사용자부터                
```     


> **확인문제: 다음 표는 주요 집계함수를 정리한 것입니다. 각 설명에 해당하는 올바른 함수명을 기호에 맞게 작성하세요.**

| 함수명 | 설명 |
|--------|------|
| SUM() | 합계를 구합니다. |
| (ㄱ) | 평균을 구합니다. |
| (ㄴ) | 최소값을 구합니다. |
| MAX() | 최대값을 구합니다. |
| (ㄷ) | 행의 개수를 셉니다. |
| (ㄹ) | 행의 개수를 셉니다 (중복은 1개만 인정). |

```
여기에 답을 적어주세요!
(ㄱ) AVG()
(ㄴ) MIN()
(ㄷ) COUNT()
(ㄹ) COUNT(DISTICT)
```


## 3. 데이터 변경을 위한 SQL문

<!-- INSERT문, UPDATE문, DELETE문에 관해 배우게 된 점을 적어주세요. -->


여기에 배우게 된 점을 적어주세요!
### INSERT문:      
테이블에 행 데이터를 입력하는 문       
테이블 이름 다음에 나오는 열은 생략 가능.    
열 이름 생략 시 VALUES 다음에 나오는 값들의 순서 및 개수는 테이블 정의 시 열 순서 및 개수와 동일해야 함          
```       
USE market_db;     
CREATE TABLE hongong1 (toy_id, INT, toy_name CHAR(4), age INT);        
INSERT INTO hongong1 VALUES (1, '우디', 25);            
```       <br />
<br />
<br />

#### AUTO_INCREMENT    
열을 정의할 때 1부터 증가하는 값 입력       
AUTO_INCREMENT로 지정하는 열은 꼭 PRIMARY KEY로 지정해줘야 함.       
```        
CREATE TABLE hongong2(          
    toy_id INT AUTO_INCREMENT PRIMARY KEY,
    toy_name CHAR(4),
    age INT);           
```         
-> 아이디 열 자동 증가로 설정     

처음 입력되는 값을 1000으로 지정하고 다음 값은 3씩 증가하도록 설정하는 방법      
```    
CREATE TABLE hongong3(          
    toy_id INT AUTO_INCREMENT PRIMARY KEY,
    toy_name CHAR(4),    
    age INT);   
ALTER TABLE hongong3 AUTO_INCREMENT=1000;        
SET @@auto_increment_increment=3;       
```      

#### 다른 테이블의 데이터를 한 번에 입력. INSERT INTO~SELECT       
```     
INSERT INTO city_popul   
    SELECT Name, Population FROM world.city;      
```       

### UPDATE문:      
행 데이터 수정해야 하는 경우      
          
한 번에 여러 열 값 변경하는 경우     
New York을 뉴욕으로, population은 0으로 설정    
```     
UPDATE city_popul    
    SET city_name = '뉴욕', population = 0    
    WHERE city_name = 'New York';     
SELECT * FROM city_popul WHERE city_name = '뉴욕';         
```        
WHERE절을 생략하는 테이블의 모든 행 값이 변경되므로 주의     

### DELETE문:        
테이블 행 데이터를 삭제해야 하는 경우     
```    
DELETE FROM city_popul      
    WHERE city_name LIKE 'New%';       
```      



# 2️⃣ 실습과제

다음 SQL 문을 작성하고 실행 결과를 확인 후 인증 사진을 아래에 업로드하세요.(market_db를 그대로 사용합니다.)

1. 모든 그룹 멤버의 정보를 조회하시오.
2. 멤버의 수가 6명 이상인 그룹 정보를 조회하시오.
3. 현재 구매 테이블에 존재하는 서로 다른 상품(prod_name)이 어떤 것이 있는지 조회하시오.
4. 총 구매 금액이 1000미만인 prod_name 중 상위 2개만 조회하시오.

<img width="1274" height="666" alt="스크린샷 2026-09-13 230903" src="https://github.com/user-attachments/assets/68139c06-b07f-401d-bf4f-c105b5b14ab2" />
<img width="1282" height="782" alt="스크린샷 2026-09-13 230819" src="https://github.com/user-attachments/assets/1bf9c43d-19d0-4214-99a8-7b3f9553d46d" />
![Uploading 스크린샷 2026-09-13 230903.png…]()
<img width="992" height="558" alt="스크린샷 2026-09-13 230945" src="https://github.com/user-attachments/assets/ce33b2d1-9cb3-4938-a0bf-00e1ee44a9ce" />

<img width="1288" height="702" alt="스크린샷 2026-09-13 231354" src="https://github.com/user-attachments/assets/db8b6050-d9b5-41c1-b709-407ce44b1789" />





### 🎉 수고하셨습니다.







# 데이터분석 6주차 정규과제

📌데이터분석 정규과제는 매주 정해진 분량의 『*혼자 공부하는 데이터 분석 with 파이썬*』 을 읽고 학습하는 것입니다. 이번 주는 아래의 **DataAnalysis_6th_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=XD65UhBMOiI&list=PLVsNizTWUw7FGzSRCkQrPEEe-ljVXgS7k&index=12
https://www.youtube.com/watch?v=NTQ5NXelOfw&list=PLVsNizTWUw7FGzSRCkQrPEEe-ljVXgS7k&index=13
-->


## DataAnalysis_6th_TIL

### 6장 복잡한 데이터 표현하기
#### 01. 객체지향 API로 그래프 꾸미기
#### 02. 맷플롯립의 고급 기능 배우기


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~81    | ✅         |
| 2주차 | p.84~151   | ✅         |
| 3주차 | p.154~219  | ✅         |
| 4주차 | p.222~279 | ✅         |
| 5주차 | p.282~325 | ✅         |
| 6주차 | p.328~379 | ✅         |
| 7주차 | p.382~430 | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->


# 1️⃣ 개념 정리 

## 01. 객체지향 API로 그래프 꾸미기

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
### pyplot 방식과 객체지향 API방식  
pyplot 방식으로 그래프 그리기는 matplotlib.pyplot에 있는 함수 사용  
함수들이 하나의 피겨 객체에 대한 상태 공유   
Axes 객체를 사용하는 객체 지향 API 방식으로 그래프 그리기   

### 그래프에 한글 출력하기   
폰트 지정하기1: font.family  
폰트 지정하기2: rc() 함수  

value_counts() 메서드는 카운트가높은 순으로 결과 내림차순 정렬   
isin() 메서드는 앞선 정렬에 있는 행일 경우 true 아니면 false   
sample() 메서드는 무작위로 행 선택  
random_state 매개변수에 임의 숫자 작성   

산점도에서 s 매개변수 값을 하나의 실수로 바꾸면 모든 마커 크기가 동일하게 변경  
하나의 열을 지정하면 그 열이 많을 수록 상대적으로 크게 그림  
alpha 매개변수는 마커의 투명도 조정. 진하기에 따라 얼마나 많이 나타난지 파악 가능  
edgecolor 매개변수는 마커 테두리 색 결정  
linewidths 매개변수는 마커 테두리 선의 두께 결정. 기본값 1.5  
c 매개변수는 산점도 색 지정. 데이터 개수와 동일한 길이의 배열을 전달하면 각 데이터를 다른 색으로 그릴 수 있음.  

컬러맵 사용하여 값에 따라 다른 색상 표현  
viridis 컬러맵, jet 컬러맵 자주 사용   


## 02. 맷플롯립의 고급 기능 배우기

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
### 하나의 피겨에 여러 개의 선 그래프 그리기  
plot() 함수를 여러 번 호출하기  
groupby() 메서드로 열을 기준으로 행 모으기   
sum() 메서드로 열의 합 구해줌  
reset_index() 메서드: 인덱스 초기화  
legend() 메서드: 범례 label 추가하면 어떤 선이 무엇을 나타내는 선인지 표시  
set_xlim 메서드: 출력할 x축의 좌표 범위 지정  
set_ylim 메서드: y축의 좌표 지정  

스택영역그래프: 하나의 선 그래프 위에 다른 선 그래프 차례대로 쌓는 것. 그래프 사이 간격이 y축의 값  
stackplot() 메서드 사용  
pivot_table() 메서드: 하나의 열을 2차원 배열로 바꾸는 것. index 매개변수와 columns 매개변수에 원본 데이터프레임 열 지정하면 각 열의 고유한 값이 피벗 테이블로 변환  
loc 매개변수로 범례 위치 지정.   

### 하나의 피겨에 여러 개의 막대그래프 그리기  
스택막대그래프: 막대그래프를 옆으로 나란히 놓치 않고 스택 영역 그래프처럼 위로 쌓은 그래프  
bottom 매개변수를 사용하여 수동으로 막대 쌓기  
cumsum() 메서드 사용하여 값 누적하기  
가장 큰 막대를 먼저 그려야 함. 그렇지 않을 경우 큰 막대가 이전에 그린 막대를 모두 덮어쓰게 됨.  
range()함수로 행 개수만큼 인덱스 번호 만들기.  for문에 reversed()함수 사용하여 인덱스 역순으로 반복   

### 원그래프 그리기  
전체 데이터에 대한 비율을 원 부채꼴로 표현(파이차트)  
원 그래프는 맷플롯립의 pie()메서드로 그릴 수 있음   
시각적으로 어떤 데이터가 더 큰 지 한 눈에 구분하기 어렵다는 단점  

autopct 매개변수: %d를 하면 부채꼴 비율이 정수로 표시  
explode 매개변수: 부채꼴 조각을 원 그래프에서 조금 떨어뜨려 시각적 부각  


### 맷플롯립으로 복잡한 그래프 그리기    
stackplot() 스택 영역 그래프  
pivot_table() 데이터 변환 
cumsum() 막대 길이 미리 누적  
pie() 원 그래프  

### 스택 막대 그래프 그리기  
plot.bar(): 막대 나란히 출력  
stacked 매개변수를 True로 지정 -> 스택 막대 그래프 그릴 수 있음  


# 2️⃣ 수행 인증

<!-- 교재에서 안내된 과정을 직접 실행해본 뒤, 진행 결과가 보이도록 4~6장의 스크린샷을 캡처하여 아래에 첨부해주세요.-->
<img width="761" height="502" alt="image" src="https://github.com/user-attachments/assets/40417490-c2d1-4351-9cef-12cd0ed6a584" />
<img width="807" height="606" alt="image" src="https://github.com/user-attachments/assets/a5dd518b-92b6-45ba-9850-02f20120a2fb" />
<img width="807" height="606" alt="image" src="https://github.com/user-attachments/assets/8d3df3c9-2555-422c-a9c8-c910d1cfcac1" />
<img width="780" height="504" alt="image" src="https://github.com/user-attachments/assets/60a365d1-9ed5-4d9e-9ece-2f69ccca8751" />



<br>
<br>

# 3️⃣ 확인 문제

## 문제 1.

> **🧚Q. 이번 주차에는 확인문제 대신 그래프 그리기 실습을 진행합니다.
4주차에서 사용했던 캐글 데이터셋을 활용하여, 다양한 요소를 포함한 복잡한 그래프를 직접 작성해주세요.**

```
여기에 코랩 링크를 첨부해주세요!
(제출 전, 코랩의 공유 설정을 ‘링크가 있는 모든 사용자가 보기 가능’으로 변경했는지 반드시 확인해주세요.)
```
<img width="985" height="492" alt="image" src="https://github.com/user-attachments/assets/b627ff37-92c4-43aa-b5bc-ab4a08820ac0" />
<img width="995" height="679" alt="image" src="https://github.com/user-attachments/assets/a56366d4-c1dc-4ff1-9d90-fc13da0322c5" />
https://colab.research.google.com/drive/1r6mlGb-mXKkyYqnJMLETf6MGpM8cI7JI?usp=sharing


### 🎉 수고하셨습니다.

# 데이터분석 5주차 정규과제

📌데이터분석 정규과제는 매주 정해진 분량의 『*혼자 공부하는 데이터 분석 with 파이썬*』 을 읽고 학습하는 것입니다. 이번 주는 아래의 **DataAnalysis_5th_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=ho0LZ6GWhtc&list=PLVsNizTWUw7FGzSRCkQrPEEe-ljVXgS7k&index=10
https://www.youtube.com/watch?v=deYY4xHsI0o&list=PLVsNizTWUw7FGzSRCkQrPEEe-ljVXgS7k&index=11
-->


## DataAnalysis_5th_TIL

### 5장 데이터 시각화하기
#### 01. 맷플롯립 기본 요소 알아보기
#### 02. 선 그래프와 막대 그래프 그리기


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~81    | ✅         |
| 2주차 | p.84~151   | ✅         |
| 3주차 | p.154~219  | ✅         |
| 4주차 | p.222~279 | ✅         |
| 5주차 | p.282~325 | ✅         |
| 6주차 | p.328~379 | 🍽️         |
| 7주차 | p.382~430 | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->


# 1️⃣ 개념 정리 

## 01. 맷플롯립 기본 요소 알아보기

# Figure 객체    
피겨.   
matplotlib 임포트 후 scatter()함수로 x축 y축 설정  alpha 매개변수로 투명도 조절    
figsize로 크기 조절. 숫자는 인치     
dpi 매개변수 지정을 통해 크기 조절 가능  
 

# rcParams 객체     
맷플롯립 그래프의 기본값 관리하는 객체   
DPI 기본값 변경 -> 해상도   
scatter.marker -> 산점도 마커 모양 변경   


# 여러 개의 서브플롯 출력하기   
서브플롯: 맷플롯립의 axes 클랙스의 객체. 하나의 서브플롯은 두 개 이상의 축을 포함.     
- 서브플롯 그리기 subplots()
axs[0]/[1] 첫번쩨/두번째 그래프
- 서브플롯 가로로 나란히 출력 subplots(1,2) <- 한 개 행, 두 개 열 생성   
     

## 02. 선 그래프와 막대 그래프 그리기

# 연도별 발행 도서 개수 구하기  
value_counts() 메서드: 한 열에서 고유한 값의 등장 횟수  
sort_index() 메서드: 인덱스 순서대로 데이터 정렬  

# 주제별 도서 개수 구하기  
주제분류번호 열 값을 받아 첫 번째 문자를 반환하는 kdx_1st_char()함수   
-> apply()메서드에 넣어 반복 적용  

# 선 그래프 그리기  
plot()함수: 선그래프   
title()함수: 그래프 제목   
xlabel()함수, ylabel()함수: xy축 이름    
linestyle 매개변수로 선 모양 지정   
color 매개변수로 색상 지정   
marker 매개변수   
xticks()함수: x축 눈금 지정   

# 막대 그래프 그리기   
bar()함수  
annontate()함수의 ha 매개변수로 텍스트 위치 조절 rigt/left   
fontsize 매개변수로 텍스트 크기 조절   
color 매개변수로 색 조정   
bar()함수에서 width 매개변수로 막대 두께 조절   
barh()함수: 가로 막대 그래프   
막대 두께 매개변수는 height 매개변수   
텍스트를 막대 중앙에 정렬할 때 va  매개변수 사용   




# 2️⃣ 수행 인증

<!-- 교재에서 안내된 과정을 직접 실행해본 뒤, 진행 결과가 보이도록 4~6장의 스크린샷을 캡처하여 아래에 첨부해주세요.-->
<img width="795" height="625" alt="image" src="https://github.com/user-attachments/assets/735715b4-0c5a-4eca-b26e-5332f29683a2" />   
<img width="795" height="625" alt="image" src="https://github.com/user-attachments/assets/0771313a-feb3-43a3-a2db-b8fd3b278d53" />  
<img width="795" height="625" alt="image" src="https://github.com/user-attachments/assets/d85d3b78-1043-4369-ab2d-a75263650610" />
<img width="795" height="625" alt="image" src="https://github.com/user-attachments/assets/daeb9cd2-c489-425f-a2b1-751a3277bf53" />





<br>
<br>

# 3️⃣ 확인 문제

## 문제 1.

> **🧚Q. 다음 데이터를 이용하여 matplotlib으로 선그래프를 그리는 코드를 작성해주세요.**
- x = [1, 2, 3, 4, 5]
- y = [2, 4, 6, 8, 10]
> 조건은 아래와 같습니다.
```
1️⃣ 제목은 "Linear Trend"로 설정해주세요.
2️⃣ x축 이름은 "X values"로 설정해주세요.
3️⃣ y축 이름은 "Y values"로 설정해주세요.
4️⃣ 마커(marker)를 포함하여 선그래프를 그려주세요.
```

```
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

plt.plot(x, y, 'o-')
plt.title("Linear Trend")
plt.xlabel("X values")
plt.ylabel("Y values")

plt.show()
```



### 🎉 수고하셨습니다.

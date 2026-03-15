# 데이터분석 2주차 정규과제

📌데이터분석 정규과제는 매주 정해진 분량의 『*혼자 공부하는 데이터 분석 with 파이썬*』 을 읽고 학습하는 것입니다. 이번 주는 아래의 **DataAnalysis_2nd_TIL**에 나열된 분량을 읽고 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 제시된 강의를 참고하여 보완하는 것이 좋습니다.

<!-- 강의 링크는 아래와 같습니다.
https://www.youtube.com/watch?v=s_-VvTLb3gs&list=PLVsNizTWUw7FGzSRCkQrPEEe-ljVXgS7k&index=4
https://www.youtube.com/watch?v=Il6L8OtNFpc&list=PLVsNizTWUw7FGzSRCkQrPEEe-ljVXgS7k&index=5
-->


## DataAnalysis_2nd_TIL

### 2장 데이터 수집하기
#### 01. API 사용하기
#### 02. 웹 스크래핑 사용하기


## Study Schedule

| 주차  | 공부 범위     | 완료 여부 |
| ----- | ------------- | --------- |
| 1주차 | p.24~81    | ✅         |
| 2주차 | p.84~151   | ✅         |
| 3주차 | p.154~219  | 🍽️         |
| 4주차 | p.222~279 | 🍽️         |
| 5주차 | p.282~325 | 🍽️         |
| 6주차 | p.328~379 | 🍽️         |
| 7주차 | p.382~430 | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->


# 1️⃣ 개념 정리 

## 01. API 사용하기

API: 두 프로그램이 서로 대화하기 위한 방법을 정의한 것. 데이터베이스의 복잡한 접근 권한을 인증된 URL을 통해 필요한 데이터에 편리하게 접근할 수 있는 방식.
HTTP: 인터넷에서 웹 페이지를 전송하는 기본 통신 방법. 웹사이트를 서비스하기 위해 웹 서버 소프트웨어를 사용하는데 엔진엑스, 아파치 등의 웹 브라우저와 통신할 때 HTTP라는 프로토콜을 사용.
웹 브라우저가 웹 서버에 웹 페이지 요청을 하고, 웹 서버는 요청에 맞는 웹 페이지를 웹 브라우저에게 전송. 

HTML: 웹 브라우저가 표시할 수 있는 문서의 한 종류, 웹 페이지를 위한 표준 언어.
HTML 같은 언어를 마크업 언어라고 부르며 div 같은 표시를 태그라고 부른다. 
HTTP 프로토콜을 사용하지만 HTML을 주고 받는 것이 아니라 CSV, JSON, XML 같은 파일 사용 (HTML 소스에서의 구조가 비교적 복잡 / 주고받는 데이터가 복잡한 구조를 가지면 버그 가능성 높다)

JSON: JavaScript Object Notation의 약자. 파이썬의 딕셔너리와 리스트를 중첩해 놓은 것과 비슷. 
중괄호를 사용하고 파이썬의 딕셔너리와 비슷하게 키와 값을 콜론(:)으로 연결. 
------
d= {"name":"혼자 공부하는 데이터 분석"}
print(d['name']) <- 파이썬은 작따, 큰따 모두 사용 가능
------- 

파이썬 객체를 JSON 문자열로 변환하는 법
json.dumps() 함수 사용
-------
import json
d_str = json.dumps(d, ensure_ascii=False)
print(d_str)
=> (출력) {"name": "혼자 공부하는 데이터 분석"}
--------
json.dumps() 함수를 사용할 때 ensure_ascii 매개변수를 False로 지정한 이유는 딕셔너리 d에 한글이 포함되어 있기 때문.
json.dumps() 함수는 아스키 문자 외의 다른 문자를 16진수로 출력하기 때문에 한글이 제대로 보이지 않음
ensure_ascii 매겨변수를 False로 지정하여 원래 저장된 문자 그대로 출력 가능. 

-----
print(type(d_str))
=> (출력) <class 'str'>
------
딕셔너리가 문자열로 바뀐 것을 확인할 수 있음. 

웹 기반 API는 전송하려는 파이썬 객체를 json.dumps() 함수를 사용하여 JSON 문자열로 변화하여 전송하지만 이 문자열을 파이썬 프로그램에 사용하려면 다시 파이썬 딕셔너리로 변경 필요

<JSON 문자열을 파이썬 객체로 변환하기>
json.loads() 함수
------
ds=json.loads(d_str)
print(d2['name'])
=> (출력) 혼자 공부하는 데이터 분석
------
print(type(d2))
=> (출력) <class 'dict'>
-----
d_str 문자열을 파이썬 딕셔너리로 변경된 걸 확인 가능.

-----
df=json.loads('{"name": "혼자 공부하는 데이터 분석", "author": "박해선", "year": 2022}')
print(d3['name'])
print(d3['author'])
print(d3['year'])
=> (출력) 혼자 공부하는 데이터 분석
박해선
2022
-------------
d3=json.loads('{"name": "혼자 공부하는 데이터 분석", "author": ["박해선", "홍길동"], "year": 2022}')
print(d3['author'][1])
=> (출력) 홍길동
--------------

<JSON 문자열을 데이터프레임으로 변환하기>
read_json() 함수
판다스는 JSON 문자열을 읽어서 데이터프레임으로 변환하는 read_json() 함수 제공. 
------
import pandas as pd
pd.read_json(d4_str)
=> (표로 출력)
------
pd.DataFrame(d4)
=> (표로 출력)
--------

<파이썬에서 XML 데이터 다루기>
XML: eXtensible Markup Language. 컴퓨터와 사람이 모두 읽고 쓰기 편한 문서 포맷을 위해 고안. 
엘리먼트들이 계층 구조를 이루면서 정보를 표현. 엘리먼트는 시작 태그와 종료 태그로 감쌈. 
태그는 < > 기호로 끝나며 태그 이름은 영문자와 숫자 사용. 시작 태그와 종료 태그의 이름 같음. 
시작태그: <name> 
종료태그: </name>
<book> 엘리먼트가 세 개의 하위 엘리먼트를 가지고  있기에 <book> 엘리먼트는 부모 엘리먼트 및 부모 노드
<name>, <author>, <year>는 자식 엘리먼트라고 한다. 

<XML 문자열을 파이썬 객체로 변환하기>
fromstring() 함수
-----------
X_str = """
<book>
  <name> 혼자 공부하는 데이터 분석</name>
  <author> 박해선</author>
  <year>2022</year>
</book?
"""
------------
-------------
import xml.etree.ElementTree as et
book = et.fromstring(x_str)
------------
-> s_str 문자열을 XML로 변환한 것. 

<자신 엘리먼트 확인하기>
findtext()
---------
book_childs = list(book)
print(book_childs)
=> (출력) [<Element 'name' at 0x7f8d78d3dc28>? <Element 'author' at 0x7f8d481ea2c8〉，
<Element 'year' at 0x7f8d481ea048>]
----------
-> <book> 엘리먼트의 자식 엘리먼트를 구하고 자식 엘리먼트에 담긴 텍스트를 읽은 것. 

--------
name, author, year = book_childs
print(name.text)
print(author.text)
print(year.text)
=> (출력) 혼자 공부하는 데이터 분석
박해선 
2022
--------------
--------------
name=book.findtext('name')
author=book.findtext('author')
year=book.findtext('year')
print(name)
print(author)
print(year)
=> (출력) 혼자 공부하는 데이터 분석
박해선
2022
-------------

<여러 개의 자식 엘리먼트 확인하기: findall() 메서드와 for 문>
동일한 이름을 가진 여러 개의 자식 엘리먼트를 찾을 때는 findall() 메서드와 for 문을 사용.
-----------
for book in books.findall('book'):
  name=book.findtext('name')
  author=book.findtext('author')
  year=book.findtext('year')
  print(name)
  print(author)
  print(year)
  print()
=> 혼자 공부하는 데이터 분석
 박해선
2022

혼자 공부하는 머신러닝+딥러닝
박해선 
2020

<공개 API로 웹에서 데이터 가져오기>
requests 패키지
get() 함수
jso() 메서드


## 02.웹 스크래핑 사용하기

웹스크래핑/웹크롤링: 프로그램으로 웹사이트의 페이지를 옮겨 가면서 데이터를 추출하는 작업

-검색 결과 페이지 가져오기
gdown 패키지를 사용해 다운로드

-데이터프레임 행과 열 선택하기: loc 메서드
loc는 메서드지만 대괄호를 사용하여 행의 목록과 열의 목록을 받음. 

-검색 결과 페이지 HTML 가져오기: request.get() 함수


HTML에서 데이터 추출하기: 뷰티플수프
-크롬 개발자 도구로 HTML 태그 찾기
-태그 위치 찾기: find() 메서드
-도서 상세 페이지 HTML 가져오기
-테이블 태그를 리스트로 가져오기: find_all() 메서드
-태그 안의 텍스트 가져오기: get_text() 메서드


데이터프레임 행 혹은 열에 함수 적용하기: apply() 메서드
첫 번째 매개변수는 실행할 함수. axis=1이면 행에 0이면 열에 적용

데이터프레임과 시리즈 합치기: merge() 함수



# 2️⃣ 수행 인증

<!-- 교재에서 안내된 과정을 직접 실행해본 뒤, 진행 결과가 보이도록 4~6장의 스크린샷을 캡처하여 아래에 첨부해주세요.-->

<img width="968" height="547" alt="Image" src="https://github.com/user-attachments/assets/48fcf162-447b-46aa-9fb8-13668acc43af" />
<img width="968" height="547" alt="Image" src="https://github.com/user-attachments/assets/2bb1288e-5a6a-4348-a8f5-22ff8300b8e5" />

<img width="968" height="547" alt="Image" src="https://github.com/user-attachments/assets/a970d44d-2dc2-4bca-9e9b-7a95b56a019e" />

<img width="1706" height="591" alt="Image" src="https://github.com/user-attachments/assets/d17241b4-ba70-425c-8f1e-ded42382a5e6" />

<img width="1706" height="591" alt="Image" src="https://github.com/user-attachments/assets/58531327-55b8-4922-9e0c-7c76ed8a0719" />


<br>
<br>

# 3️⃣ 확인 문제

## 문제 1.

> **🧚Q. 다음 중 BeautifulSoup 외에 웹 스크래핑에 사용할 수 있는 파이썬 패키지로 가장 적절한 것은 무엇인가요?**

```
1️⃣ NumPy  
2️⃣ Scrapy  
3️⃣ Matplotlib  
4️⃣ Scikit-learn  
```

```
여기에 선택한 답과 그 이유를 간단히 서술해주세요!
```
Scrapy / requests와 뷰티플수프를 합쳐놓은 것과 비슷하게 작동 가능. 


### 🎉 수고하셨습니다.

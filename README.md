# 도서 정보 및 리뷰 데이터 기반 추천 프로젝트
<br />

# 프로젝트 개요

## 🚀프로젝트 소개
온라인 서점의 책정보, 리뷰 정보를 수집하여 수집된 데이터를 기반으로 책 분석, 개인 맞춤 책 추천 서비스를 제공합니다.

## 👍프로젝트 목표

- 크롤링 능력 향상
- 데이터 전처리, 분석 프로젝트 경험

## 📖 프로젝트 기획

- 피그마를 활용한 브레인스토밍 <br />
![](https://velog.velcdn.com/images/devysy55/post/d5d8f945-4169-4617-a294-cfc0be506970/image.png)

- 구글 공유문서 활용 데이터 기획 <br />
![](https://velog.velcdn.com/images/devysy55/post/3eb3a3ba-b596-49a8-a04d-0b55a2c10f34/image.png)


 
***
# 데이터 수집
 
## ✨수집 기준
 
1. 알라딘: 베트스셀러>역대베스트 2015, 2019~2023 총 6개년 1위 ~ 200위 책 
2. 교보문고: 베스트셀러>종합 연간 베스트 2019~2023 총 5개년 1위 ~ 200위 책

## 🧞‍알라딘 
### 리뷰 수집 
#### 윤소영
![](https://velog.velcdn.com/images/devysy55/post/d8cd3c96-ec7f-47c9-b7a0-e635de06f0f4/image.png) <br />
**1. 기본 정보**<br />
알라딘 리뷰는 "100자평", "마이리뷰" 2가지 형태의 리뷰를 제공하고 있다. 리뷰는 한 번에 5개씩 제공하고 있으며 추가 리뷰를 보기 위해서는 "더보기" 버튼을 계속 클릭해야하는 어려움이 있었다.<br />
**2. 수집 방식**<br />
앞서 설명한 어려움으로 인해 크롤링이 아닌 알라딘 내부 API를 활용하였다. 각각 다른 API를 사용하였으며 API 호출 시 미리 수집된 a_isbn과 iteml_id를 파라미터로 사용하였다. 마이리뷰의 경우 헤더 정보를 함께 전달해야했다. response는 html형식이었으며 파싱 작업을 통해 원하는 정보를 csv파일로 저장하였다. <br />
**3. 데이터 병합** <br />
100자평 리뷰, 마이리뷰는 저장된 csv파일이 분리되어있어 이를 병합하는 작업이 필요했다. 파이썬의 pandas의 merge, concat 메소드를 활용하여 병합하였다


### 책 상세 정보 수집 
#### 윤소영
**1. 기본 정보** <br />
데이터 수집 시 수집 대상 책 리스트는 알라딘에서 제공하는 역대베스트 xls 파일을 사용하였다. 해당 파일에서 제공하지 않는 정보는 각 책별 상세 정보에서 책소개, ISBN, 쪽 수, 카테고리, 알라딘ISBN을 수집하였다 <br />
**2. 수집 방식**<br />
selenium을 활용하여 동적 크롤링을 진행하였고 수집된 html을 파싱하여 원하는 정보를 csv파일로 저장하였다.<br />
**3. 데이터 병합**<br />
수집된 데이터는 팀원에게 전달하여 다른 책 정보와 병합을 요청하였다.<br />

### review 수 가져오기
#### 최은서


- 아래 사진 속 ‘(286)’과 같은 도서 별 리뷰 수를 추출할 것. 

![](https://velog.velcdn.com/images/eschoi2402/post/838e9b6f-787c-4627-a02a-43eee86928bd/image.png)

- 다른 파일과 병합 시 공통칼럼이 존재해야하므로 각 도서의 isbn을 함께 추출할 것.
- 추가로 제목과 작가명, 판매가격도 함께 추출.
![](https://velog.velcdn.com/images/eschoi2402/post/e19c390d-6806-4bd9-bec0-1a12c8e205cb/image.png)


- 알라딘 웹페이지에는 한 페이지 당 지정 연도의 50위까지만 보여줌. 따라서, url의 ‘year’값과 ‘page’값을 변경해 리뷰 수를 크롤링할 것.
    - ex) page=1 → 1-50위, page=2 → 51-100위 등


### 파일 병합
#### 최은서

- 크롤링을 통해 얻은 정보들이 담긴 4개의 파일을 공통칼럼 기준으로 병합한다.
- 'inner join'을 통해 겹치지 않는 값은 누락시킨다.
- 최종적으로 병합된 파일의 컬럼은 아래와 같다.
 ![](https://velog.velcdn.com/images/eschoi2402/post/db4982c4-86eb-44bd-92ef-ea3ae205de01/image.png)

#### 전처리

1. 전처리할 파일의 정보를 확인한다.(첫 번째 행 출력, 행/열 수 출력, 인코딩 등)
![](https://velog.velcdn.com/images/eschoi2402/post/3c7aba9b-7b5b-482f-a26f-ab297f9d3a17/image.png)

2. 각 컬럼의 데이터타입을 파악한다.
![](https://velog.velcdn.com/images/eschoi2402/post/83fcf53b-b1d6-4bf4-bf4c-ce59d3a44892/image.png)

3. 필요에 따라 컬럼의 데이터타입을 변경한다. 
4. 쉼표, 단위 등을 제거한다.

   

## 📚교보문고
### 교보 리뷰수집(k_review_crolling)

#### 장지원
교보 상세페이지에서 리뷰가 있는 부분 api url 주소를 사용하였다. <br />
![](https://velog.velcdn.com/images/jiw0707/post/26adb92d-9334-4496-b0ae-4e0e42398c08/image.png) <br />
page 번호와 saleCmdtid만 변경되는 부분을 이용하여 함수를 만들어 사용하였다. 이 둘을 순환문을 사용하여 자동으로 모든 리뷰가 추출될 수 있게 하였다.<br />
page번호 범위는 1페이지부터 10페이지 까지로 지정해주었고,<br />
saleCmdtid 범위는 교보에서 제공하는 연간 베스트 순위 책정보 csv 파일에서 추출하여 리스트를 만들어주었다.<br />
***
---
### 교보문고 연간 베스트셀러 정보 수집
#### 곽태호
- 교보문고 페이지를 동적 크롤링으로 진행했다.
- 수집한 데이터:
19년도 - 23년도 연간 베스트 셀러의 
책 제목, 책 내용, 작가, 작가 정보, 서평, 가격, 리뷰 수, 총 평점, isbn, 페이지 수, 카테고리, saleCmdtid(책 정보 관련 페이지의 주소 끝자리)
- 연간 베스트셀러는 약 200권으로, 총 권수 800권 정도의 책 데이터를 추출했다.
- 이 중 작가 정보, 서평은 '펼치기'를 눌러야 텍스트 전체가 나와 추가로 button 함수를 넣었다.
---

![](https://velog.velcdn.com/images/taehokk/post/5b83bb8a-aab4-4be2-8de9-da16d2b92fb4/image.png)
###### 펼치기 누르기 전
---

![](https://velog.velcdn.com/images/taehokk/post/cab79077-6b77-43b9-931d-d630871255f1/image.png)
###### 펼치기 누른 후
---


- 전처리
1. 데이터 전처리 전에 먼저 교보문고, 알라딘 두 데이터의 칼럼 이름 일치시켰다.
2. 두 데이터를 합칠 때 concat 함수를 사용했다.
3. concat으로 인해 발생한 데이터 중복을 제거했다.
4. isbn이 null인 데이터는 사용할 수가 없어 제거했다.
5. 책 제목의 ()안에 필요없는 부분이 많아 ()안에 있는 문자열을 제거했다.
   (예시: 돈의 속성(300쇄 리커버에디션))
---


# 데이터 분석

## 평점/키워드 기반 책 출력(지원_Review_based_random_output)
#### 장지원

1. 평점 기반 랜덤 출력 <br />
   긍정적 평가 - 평점 5점 초과 <br />
   부정적 평가 - 평가 5점 이하 <br />
   가장 긍정적/부정적 평가를 받은 10개의 ISBN선택한다. <br />
   10개의 ISBN의 가지고 있는 수백개의 리뷰 중 1개를 랜덤으로 선택하여 출력된다. <br />
   긍정/부정 각각 10개의 행을 가진 데이터 프레임이 출력된다. <br />
   ![](https://velog.velcdn.com/images/jiw0707/post/7322bb19-0d05-46a2-9465-2d17e0efc0df/image.png)![](https://velog.velcdn.com/images/jiw0707/post/ae2e905a-0a4d-410c-8f6a-5abbc6a0b2a3/image.png)


2. 키워드/평점 기반 랜덤 출력<br />
   정해진 키워드를 통해 긍정적인 평가가 많은 10권, 부정적인 평가가 많은 10권 랜덤 출력한다.<br />
   2-1.긍정 키워드와 부정 키워드를 코드 내에서 미리 지정한다.<br />
   2-2.정해진 긍정/부정 키워드가 리뷰에 포함된 100개의 ISBN을 선택한다.<br />
   그 중 중복되지 않는 ISBN을 골라 리뷰평점이 5점 초과인 10개의 ISBN을 선택한다.<br />
   2-3. 10개의 ISBN의 가지고 있는 수백개의 리뷰 중 1개를 랜덤하게 출력한다.<br />
   ![](https://velog.velcdn.com/images/jiw0707/post/e3340bda-5c95-4d5c-8ec0-e4e3b38bc7a8/image.png)![](https://velog.velcdn.com/images/jiw0707/post/39b28667-bf11-449a-8bcc-3a821e6e2e81/image.png)

3. 키워드/평점 기반 랜덤 출력<br />
   3-1.긍정, 부정 키워드를 각각 입력받는다.<br />
   3-2.정해진 긍정/부정 키워드가 리뷰에 포함된 100개의 ISBN을 선택한다.<br />
   그 중 중복되지 않는 ISBN을 골라 리뷰평점이 5점 초과/5점 이하인인 10개의 ISBN을 선택한다.<br />
   10개의 ISBN의 가지고 있는 수백개의 리뷰 중 1개를 랜덤하게 선택해 긍정/ 부정 데이터 프레임을 만든다.<br />
   3-3.작가 정보가 들어있는 csv파일에서 ISBN을 기준으로 중복을 제거 한다.<br />
   3-4.만들어진 데이터 프레임에 ISBN을 기준으로 작가정보를 추가하여 출력한다.<br />
   ![](https://velog.velcdn.com/images/jiw0707/post/dff99875-9e82-4d45-88bb-e74c06898899/image.png)![](https://velog.velcdn.com/images/jiw0707/post/6de2d155-d78f-4f79-acb5-91cf9b7db777/image.png)![](https://velog.velcdn.com/images/jiw0707/post/d9036b6d-ab67-4146-b324-b1e636f5ba74/image.png)

4. 키워드/평점 기반 랜덤 출력(일반 리뷰에서 찾기)<br />
   4-1. 키워드 하나를 입력 받는다.<br />
   4-2.정해진 해당 키워드가 리뷰에 포함된 100개의 ISBN을 선택한다.<br />
   그 중 중복되지 않는 ISBN을 골라 리뷰평점이 5점 초과/5점 이하인인 10개의 ISBN을 선택한다.<br />
   4-3. 10개의 ISBN의 가지고 있는 수백개의 리뷰 중 1개를 랜덤하게 선택해 긍정/ 부정 데이터를 출력한다.<br />
   ![](https://velog.velcdn.com/images/jiw0707/post/e235db45-70ef-4634-a5a9-118e96530fce/image.png)![](https://velog.velcdn.com/images/jiw0707/post/8c744b13-9584-4551-8e89-8aa4dca2fceb/image.png)

5. 키워드/평점 기반 랜덤 출력(워드 리스트 사용)<br />
   5-1. 리뷰CSV 파일에서 약 4만개의 행 중 리뷰평점이 10점 이상인 행을 선택해 리뷰에 있는 단어를 추출한다.<br />
   5-2.추출한 단어에서 모든 명사 형태소를 추출하고 한글자로 이루어진 단어와 출현 빈도가 100회 이하인 단어들을 삭제하고 객체 상태인 단어들을 리스트로 만든다.<br />
   5-3.만든 단어 리스트 중 부정적 키워드에 가까운 단어들을 모아 불용어 사전을 만든다.<br />
   5-4.입력 받은 키워드가 리스트에 있는지 확인한다.<br />
   리스트에 있다면 리뷰에서 키워드가 포함된 행을 필터링하여 선택한다.<br />
   필터링된 행 중 랜덤으로 100개의 행을 선택하고 리뷰 평점이 7점 이상인 10개의 행을 추출한다.<br />
   작가 정보를 추가하여 출력한다.<br />
   ![](https://velog.velcdn.com/images/jiw0707/post/a69a625f-c245-4789-af1c-4ebf0539b8a6/image.png) - 단어리스트
   ![](https://velog.velcdn.com/images/jiw0707/post/3c9f513f-caa5-48e7-8eee-e03bd8e59978/image.png)



---
### 유사도 코드를 바탕으로 시각화를 진행 (소영이 누나 코드)
#### 곽태호
- 키워드를 통해 관련 책 시각화
- 키워드: 데이터, 영어, 수학

- 유사도가 높은 책 5권 추출하여 bar차트와 파이 차트 추출 <br />
![top_books](https://github.com/pladata-encore/DE30-3-personal_book_recommendation/assets/150890899/18298801-f3bd-4641-96af-7791e11707b6)

![top_books_pie](https://github.com/pladata-encore/DE30-3-personal_book_recommendation/assets/150890899/eee21a8b-a812-47ba-a3ee-5c2f8c62a89e)

- 위의 5권의 가격을 bar차트로 추출 <br />
![book_prices](https://github.com/pladata-encore/DE30-3-personal_book_recommendation/assets/150890899/2e3320b2-2e4b-4506-b6bd-c7dbe67db768)


- 위의 5권의 총 평점 그래프 추출 <br />
![ratings_bubble](https://github.com/pladata-encore/DE30-3-personal_book_recommendation/assets/150890899/cebf3a0f-06e7-4bd4-b61a-afb110ebda25)


- 위의 5권의 관련 문장 추출 <br />

![스크린샷 2024-03-19 180002](https://github.com/pladata-encore/DE30-3-personal_book_recommendation/assets/150890899/b014a85f-7c5b-4816-bc00-f93d4cb6ad6b)
---

### 책소개/작가소개/서평 기반 키워드 도서 추천 시스템
#### 최은서

- 책소개, 작가소개, 서평이 포함된 알라딘 교보문고 통합 북리스트 테이블을 통해 키워드 기반 도서 추천 시스템을 구축한다. 
- 추천 시스템 진행 방식은 아래와 같다. 

1. 사용자가 키워드를 검색할 컬럼을 선택한다. 

![](https://velog.velcdn.com/images/eschoi2402/post/3ab18090-285f-4857-b2e9-8cce0906a679/image.png)

2. 컬럼 선택 후 원하는 키워드를 입력한다. 

![](https://velog.velcdn.com/images/eschoi2402/post/6d360889-5e77-4771-bc40-74e63477ee2f/image.png)

3. 해당 키워드를 가장 많이 보유한 상위 5권의 책 제목이 출력된다. 

![](https://velog.velcdn.com/images/eschoi2402/post/0d51045a-ece8-4208-b021-60be3c129528/image.png)

<br />
<br />
<br />

---

### 키워드 입력을 통한 책추천
#### 윤소영
- 활용 데이터: 수집된 데이터 중 리뷰DB의 comment 데이터 활용<br />
- 동작방식: 입력한 키워드를 기반으로 수집된 리뷰 데이터를 분석하여 사용자에게 적합한 책을 추천하는 프로세스를 구현하였습니다. 키워드는 쉼표(,)로 구분하여 여러개 입력할 수 있습니다.<br />
![](https://velog.velcdn.com/images/devysy55/post/c8a12905-8910-4e68-ae47-ef2045be53d2/image.png)<br />

- 분석 방식  <br />
   -  키워드와 리뷰 간의 유사도 계산은 TF-IDF 벡터라이저를 사용하였으며 코사인 유사도를 계산하여 각 리뷰마다 유사도 점수를 추출하였습니다.<br />
    - 유사도 점수를 기반으로 각 책별로 유사도의 합을 계산하고, 이를 내림차순으로 정렬하여 상위 3권의 책을 시각화하였습니다.<br />
    - 추가적으로 유사도 높은 리뷰의 비율이 높은 책 상위 3권의 책도 시각화하였습니다.<br />
- 인사이트 도출<br />
    - '각 책별 유사도 합을 계산하는 방식'과 '유사도 높은 리뷰의 비율을 계산하는 방식' 2가지를 활용하였는데 테스트 결과 후자가 더 유의미한 추천을 제공하였습니다.<br />
- 결과(입력한 키워드: "눈물이 줄줄")<br />
![](https://velog.velcdn.com/images/devysy55/post/c139e900-b355-491c-a1bd-9aed4e2a5f67/image.png)
![](https://velog.velcdn.com/images/devysy55/post/71c740b1-eb2b-4111-901e-1c8a36d51855/image.png)


### 리뷰 수, 리뷰 내용 관련 분석
#### 윤소영

#### 1. 리뷰 수 상위 도서 검색
- 숫자 입력을 통해 리뷰 수 상위 도서를 원하는 수만큼 볼 수 있다.
- 범위 입력을 통해 볼 수 있는 기능과 순위 도서 정보를 볼 수 있도록 고도화할 예정이다.
![](https://velog.velcdn.com/images/devysy55/post/19d7012b-cdee-4a79-b404-631f78f5c302/image.png)
#### 2. 리뷰에서 많이 사용되는 단어 원하는 조건으로 검색
 - 총 3가지 input 값을 받아 3단계 맞춤 검색을 구현하였다. 
 - 1단계로 빈도수가 많은 문장의 최소 글자수를 설정할 수 있게하여 자주 반복되는 짧은 문장을 필터할 수 있게 하였다. 
- 2단계는 보기 원하는 순위 범위를 지정할 수 있게 하였다. 100~110위 등 원하는 순위의 값을 범위로 입력하여 볼 수 있다
- 마지막으로 원하는 문장을 입력하면 해당 문장이 포함된 리뷰가 검색되는 기능을 구현하였다. 해당 기능은 실제로 사용하다 전체 리뷰 내용이 궁금해서 넣었다.
 ![](https://velog.velcdn.com/images/devysy55/post/55d150cb-8bd0-45e6-82b5-63cf2bd7355c/image.png)

    








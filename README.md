# 도서 정보 및 리뷰 데이터 기반 추천 프로젝트
<br />

# 프로젝트 개요

## 🚀프로젝트 소개
온라인 서점의 책정보, 리뷰 정보를 수집하여 수집된 데이터를 기반으로 책 분석, 개인 맞춤 책 추천 서비스를 제공합니다.

## 👍프로젝트 목표

- 크롤링 능력 향상
- 데이터 전처리, 분석 프로젝트 경험

## 📖 프로젝트 기획

- 피그마를 활용한 프레인 스토밍
![](https://velog.velcdn.com/images/devysy55/post/d5d8f945-4169-4617-a294-cfc0be506970/image.png)

- 구글 공유문서 활용 데이터 기획
\
![](https://velog.velcdn.com/images/devysy55/post/3eb3a3ba-b596-49a8-a04d-0b55a2c10f34/image.png)


 
***
# 데이터 수집
 
## ✨수집 기준
 
1. 알라딘: 베트스셀러>역대베스트 2015, 2019~2023 총 6개년 1위 ~ 200위 책 
2. 교보문고: 베스트셀러>종합 연간 베스트 2019~2023 총 5개년 1위 ~ 200위 책

## 🧞‍알라딘 
### 리뷰 수집 
#### 윤소영


### 알라딘 책 추가 정보 수집
 

## 📚교보문고
### 교보 리뷰수집(k_review_crolling)
#### 장지원
교보 상세페이지에서 리뷰가 있는 부분 api url 주소를 사용하였다. <br />
![](https://velog.velcdn.com/images/jiw0707/post/26adb92d-9334-4496-b0ae-4e0e42398c08/image.png) <br />
page 번호와 saleCmdtid만 변경되는 부분을 이용하여 함수를 만들어 사용하였다. 이 둘을 순환문을 사용하여 자동으로 모든 리뷰가 추출될 수 있게 하였다.<br />
page번호 범위는 1페이지부터 10페이지 까지로 지정해주었고,<br />
saleCmdtid 범위는 교보에서 제공하는 연간 베스트 순위 책정보 csv 파일에서 추출하여 리스트를 만들어주었다.<br />
***
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

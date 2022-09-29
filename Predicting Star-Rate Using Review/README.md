## Prediction Star-Rate Using Review
Data : Web crawling at Musinsa's review, star_rate

Model : BERT multilingual model with Hugging Face API, KoBART model with github(SKT-AI)

Purpose : Sentiment Analysis review, Make reliable Star_rate model

<br><br>



## 개요

인터넷에서 상품을 구매할 때 소비자의 큰 결정요인 중 하나는 실제로 구매한 고객들의 리뷰입니다.

또한 상품이 나타나는 순서 및 인기요인을 판가름하는 기준은 별점입니다.

그러나 모든 리뷰에서 **긍정리뷰+긍정별점** , **부정리뷰+부정별점**이 매칭되지는 않습니다.

1차적으로 기본적인 긍부정을 표현하는 감성분석을 bert모델을 이용해 시도해보고

2차적으로 보다 신뢰성 있는 리뷰 및 별점을 얻기 위해 kobert모델을 이용해 학습하여

임의의 리뷰를 작성했을때 자동적으로 그에 맞는 **실질별점**을 만들어보고자 프로젝트를 진행했습니다.

<pre>
고객이 작성한 리뷰에 따라 자동적으로 문맥에 맞는 실질적인 별점 부여 시스템 구축
</pre>

<br><br>

## 수집 및 전처리

Musinsa 2022년도 1~6월 상품 페이지에서 약 35만개의 평점과 별점을 크롤링

|평점 5|평점 4|평점 3|평점 2|평점 1|
|---|:---|:---|:---|:---|
|298540|39242|5332|563|463|


하지만 데이터 중 5점의 별점이 압도적으로 많은 **imbalance data**였고 이를 해결하기 위해 네이버 쇼핑 페이지에서

1~4점의 별점 및 리뷰를 추가적으로 크롤링


|평점 5|평점 4|평점 3|평점 2|평점 1|
|---|:---|:---|:---|:---|
|298324|56587|18658|2632|2351|

그러나 여전히 학습을 진행하기엔 1~3점 사이의 데이터가 부족했고 이를 보완하기 위해 EDA (Easy Data Augmentation) 방식을 차용하여

RI, RR, RD 방식으로 각 별점당 4만개씩 Data Augmentation을 진행.

<br><br>

## 모델 학습

1차 감성분석 모델은 긍부정 9만개의 데이터셋으로 학습을 진행,

2차 실점별점 평가 모델은 각 라벨당 4만개씩 총 16만개의 데이터셋으로 학습을 진행


<br><br>


## 참고 자료

https://github.com/namwootree

https://github.com/SKT-AI/KoBART  

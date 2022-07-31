---
title : "🧩 Data Mining (18) - Preprocessing_11 : Data Reduction - PCA_2"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Preprocessing, PCA, Dimensionality]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-07-31
last_modified_at: 2022-07-31 
---   
  
* * *  

🧩 저번 포스팅에서는 PCA의 개념에 대해서, 그리고 특히 그 특징에 대해서 자세히 알아보았다. 최대한 내가 공부하면서 궁금했던 점, 그리고 검색을 해도 잘 모르던 내용을 중심으로 다루어 봤는데 어땠을 지 모르겠다. 이번 포스팅에서는 저번 학기에 진행한 데이터마이닝 프로젝트를 통해 PCA 분석을 구현하는 방법을 살짝 알아보도록 하자.  

* * *  


## 1. PCA 코드 구현  

🧩 프로젝트를 위해 사용한 데이터는 캐글에서 구한 [Cardiovascular Disease dataset](https://www.kaggle.com/datasets/sulianova/cardiovascular-disease-dataset) 이다. 궁금한 분은 링크를 걸어두었으니 한번 확인해 보면서 포스팅을 봐도 좋을 것 같다. 심혈관 질환의 유무를 통해 질병의 발병에 영향을 미치는 여러가지 요인들을 총해 최종 질병 유무를 확인하는 것이 프로젝트의 목적이었다. 따라서 질병의 유무를 가장 잘 나타내는 특징을 선택하기 위해 여러 연관관계 분석 방법을 실험해봤으며, 그 중 하나가 오늘 살펴볼 PCA 이다.  

🧩 PCA분석을 위해 sklearn.decomposition 모듈의 PCA 라이브러리를 사용했으며, 시각화를 위해서는 plotly 공식 홈페이지를 참고했다.  

* * *  


### 🚩 데이터 확인  


<p align="center"><img src="https://user-images.githubusercontent.com/65170165/182029062-97437104-75fb-4903-9fc1-e980792ba49e.png" width="800" /></p><br>  


- 70000명의 조사군을 대상으로 12개의 attribute와 심혈관 질환의 유무를 나타내는 cardio라는 attribute로 데이터가 구성되며, cardio는 0인 경우 질병이 없음을, 1인 경우 질병이 있음을 의미한다.<br>  

* * *  

### 🚩 PCA 구현 및 시각화_Dimension 3  

🧩 먼저 코드부터 확인해보도록 하자🙄.  

```py
# target과 feature data 설정
# cardio가 0인 object는 'N' 으로 변환
# cardio가 1인 object는 'Y' 로 변환

cardio_target = cardio['cardio'].copy()
cardio_target[cardio_target==0] = 'N'
cardio_target[cardio_target==1] = 'Y'
cardio_feat = cardio.drop('cardio',axis = 1)
```  
```py
# sklearn.decomposition 모듈의 PCA library 임포트
# pca.fit_transform() : cardio[features]를 scaling 한 뒤에 principal component로 변환
# pca.explained_variance_ratio_ : dimension에 따른 variance 설명 정도

pca = PCA()
components = pca.fit_transform(cardio_feat)

# PCA 결과 시각화

labels = {
    str(i): f"PC {i+1} ({var:.1f}%)"
    for i, var in enumerate(pca.explained_variance_ratio_ * 100)
    }

fig = px.scatter_matrix(
    components,
    labels=labels,
    dimensions=range(3),
    color=cardio_target, opacity = 0.5
    )

fig.update_traces(diagonal_visible=False)
fig.show()
```  


- 앞선 포스팅에서도 언급했듯이, PCA과정에서 만들어지는 Principal Component의 수에 따라서 원본 데이터의 variance 설명 정도가 결정되기 때문에 이 dimension을 결정하는 변수가 존재한다. 위 코드에서 <a>dimensions = range(3)</a>가 그 변수이며, 이를 통해 PCA 결과를 시각화하면 아래와 같다.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/182030152-33fa0794-6cf4-44b3-ae93-a5ad30fdc53d.png" width="1000" /></p><br>  

- 그 결과 target으로 설정한 cardio attribut가 각각 3개의 차원에서 설명되는 것을 확인할 수 있으며, PC1과 PC2에서 대부분의 variance가 설명되는 것을 확인할 수 있다🙃. PCA를 공부한 분이라면 아시겠지만 위의 결과는 target label에 따라 선명하게 분류된 경우는 아니다. 각 attribute에 따라 target label이 명확하게 결정된다면, 위의 경우처럼 점들이 겹치기보다는 명확히 구분되는 결과가 나오게 되며, PC1에서 90%가 넘는 설명정도를 가진다. 하지만 이는 데이터의 차이라고 볼수 있기 때문에, 그렇게 신경쓸 부분은 아닐 것이라 생각하고 프로젝트를 진행했다.<br>  

- 이번에는 dimension이 4인 경우를 살펴보도록 하자.  

* * *

### 🚩 PCA 구현 및 시각화_Dimension 4  

```py
# 사용하려는 principal componenet 개수 정의

n_components = 4


# sklearn.decomposition 모듈의 PCA library 임포트. principal componenet 개수 정의.
# pca.fit_transform() : cardio[features]를 scaling 한 뒤에 principal component로 변환
# pca.explained_variance_ratio_ : dimension에 따른 variance 설명 정도

pca = PCA(n_components=n_components)
components = pca.fit_transform(cardio)


# PCA 결과 시각화

total_var = pca.explained_variance_ratio_.sum() * 100

labels = {str(i): f"PC {i+1}" for i in range(n_components)}

fig = px.scatter_matrix(
    components,
    color=cardio_target,
    opacity = 0.5,
    dimensions=range(n_components),
    labels=labels,
    title=f'Total Explained Variance: {total_var:.2f}%',
    )

fig.update_traces(diagonal_visible=False)
fig.show()
```  

- 위의 코드는 앞선 코드와 달리 <a>n_components</a> 변수를 통해 princiapl component의 개수를 미리 설정해두고 PCA를 진행한다. 그 결과는 아래 그림과 같다.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/182030776-dce485b0-cced-4163-b286-8a7d341b9e74.png" width="1000" /></p><br>  

- PC4 까지 사용한 경우에 원본 데이터의 variance를 99.58% 까지 설명하는 것을 확인했고, 이에 PCA 분석을 위해 dimension을 4로 설정하기로 했다. 당연히 PC의 수가 늘어날수록 설명 정도는 증가할 것이기에, 이를 확인해보기 위해서 시각화를 진행하였다.  

```py
# dimension에 따른 variance 설명 정도의 누적합 시각화

pca = PCA()
pca.fit(cardio)
exp_var_cumul = np.cumsum(pca.explained_variance_ratio_)

px.area(
    x=range(1, exp_var_cumul.shape[0] + 1),
    y=exp_var_cumul,
    labels={"x": "# Components", "y": "Explained Variance"}
)
```  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/182031175-709f8b31-04fe-4898-bf2a-79cbce30d177.png" width="1000" /></p><br>  

- 이 결과를 토대로 dimension을 4로 설정해서 각 attribute 간의 연관관계를 알아볼 것이다.  

* * *  

### 🚩 attribute 연관관계 파악  

🧩 앞서 설명한 PCA에 대한 개념만 가지고서 실제로 연관관계를 어떻게 분석하는지 알기는 어렵다. 이를 위해 사이킷런과 plotly 에서는 각 attribute의 방향성을 파악하기 위한 여러 기능을 제공하는데, 아래 코드를 보고 알아보도록 하자.  

```py
# vardiance를 설명하는 데 사용된 original attribute vector의 방향성 파악

X = cardio[cardio_feat.columns]

pca = PCA(n_components=4)
components = pca.fit_transform(X)

loadings = pca.components_.T * np.sqrt(pca.explained_variance_)

fig = px.scatter(components, x=0, y=1, color=cardio_target, opacity = 0.5)

for i, feature in enumerate(X):

    fig.add_shape(
        type='line',
        x0=0, y0=0,
        x1=loadings[i, 0],
        y1=loadings[i, 1],
        line=dict(color="springgreen",width=3.5)
    )

    fig.add_annotation(
        x=loadings[i, 0],
        y=loadings[i, 1],
        ax=0, ay=0,
        xanchor="center",
        yanchor="bottom",
        text=feature,
        font = {'color':'white'},
        bgcolor = 'grey'
    )

fig.show()
```  

- loadings 변수를 통해 각 attribute vector의 방향을 나타낼수 있도록 했고, for 문을 사용해서 모든 point와 vector를 시각화했다. 그 결과는 아래와 같다.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/182031756-548a2f09-6240-4dbe-b935-e1b1c091db84.png" width="1000" /></p><br>  

- 이 결과만 가지고 정확한 attribute의 방향성을 파악하기에는 각 vector가 너무 겹쳐있기 때문에, plotly에서는 이를 확대해서 볼 수 있는 기능을 제공한다. 확대해보면 다음과 같다.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/182031923-4b6326e8-62d1-47c5-a9aa-a05544d1403c.png" width="1000" /></p><br>  


🧩 PCA 분석의 결과 서로 가장 연관관계가 가장 높은 attribute는 다음과 같이 결정됐다.<br>  


<center><a><b>ap_hi, ap_lo, BMI, gluc, cholestero</b></a></center>  

* * *  

### 🚩 PCA DataFrame  

🧩 마지막으로 위의 결과 선택된 <a>[ap_hi, ap_lo, BMI, gluc, cholestero]</a> attribute를 가지고 PCA DataFrame을 만들어보자🙂<br>.  


```py
# PCA Dataframe 출력

pca = PCA(n_components=n_components)
components = pca.fit_transform(cardio)
PCA_df = pd.DataFrame({'PC1' : components[:,0],
             'PC2' : components[:,1],
             'PC3' : components[:,2],
             'PC4' : components[:,3],
             'cardio' : cardio['cardio']})
PCA_df
```  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/182032289-57f4c876-f37d-4cb3-9575-0af0ec376a15.png" width="700" /></p><br>  

- 위의 데이터프레임을 보면 처음에 70000 object가 64500 object로 변한 것을 확인할 수 있는데, 이는 outlier들을 제거하는 과정에서 수가 줄어든 것이다.  

* * *  

## PCA 정리  

🧩 앞선 포스팅과 이번 포스팅의 결과 PCA에 대한 요약은 아래와 같이 정리할 수 있다.  

- 그리고 그 새로운 attributes가 새로운 축인 principal component로 정의됨.  
- 기존의 데이터들은 새로운 축 PC1, PC2...에서 새로운 좌표를 가지게 됨.<br>  

- 새로운 축들을 만든 뒤에 그 축들을 기준으로 원래 데이터의 variance를 잘 설명하는 순서대로 번호를 매김.  
- 대부분의 variance가 PC1과 PC2만 가지고서 설명이 가능함.  
- 원하는 정도까지만 variance를 설명하면 되고, 이를 만족하는 Principal Component까지만 선택할 것이므로, 선택과정에서 Dimensionality Reduction.<br>  

- attribute vector의 방향성을 기준으로 서로 연관관계가 있는 attribute를 알아낼 수 있음.  

* * *  

🧩 이렇게 해서 Preprocessing에서 가장 중요한 개념이라고 할 수 있는 PCA 분석을 모두 알아보았다. 개념 자체가 그렇게 쉽지는 않지만 여러 라이브러리들에서 이 분석 방법을 지원하고 있기 때문에 그렇게 겁먹지 않아도 될 것 같다👍.  

🧩 프로젝트 진행 과정에서 도움을 받은 사이트와 내 블로그의 plotly 라이브러리 포스팅을 공유할테니 궁금하신 분들은 더 참고하시면 좋을 것 같다🙃🙂.  

[📝 PCA Visualization in Python](https://plotly.com/python/pca-visualization/)  

[📝 Plotly 시각화](https://nyamin9.github.io/pandas_visual/plotly/)  

[📝 Plotly for문](https://nyamin9.github.io/pandas_visual/plotly_for_loop/)  

[📝 PCA 개념](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-10/)  

🧩 다음 포스팅에서는 Preprocessing의 마지막 개념인 Data Transformation에 대해 알아보자🏃‍♂️🏃‍♂️🏃‍♂️.  

* * *  

<div style="text-align: left">💡위 포스팅은 한국외국어대학교 바이오메디컬공학부 고윤희 교수님의 [생명정보학을 위한 데이터마이닝] 강의 내용을 바탕으로 함을 밝힙니다.</div>

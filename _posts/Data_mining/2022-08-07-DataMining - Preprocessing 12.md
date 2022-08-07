---
title : "🧩 Data Mining (19) - Preprocessing_12 : Data Transformation"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Preprocessing, Data Transformation]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-08-07
last_modified_at: 2022-08-07 
---  
* * *  

🧩 오랜만에 데이터마이닝 포스팅이다. 날도 덥고, 이래저래 친구들도 만나느라 그동안 살짝 뜸했는데 앞으로 더 중요한 내용들이 많기 때문에 다시 열심히 업로드할 예정이다🏃‍♂️🏃‍♂️.  

🧩 이번 포스팅에서는 데이터 전처리의 마지막 개념인 <a>Data Transformation</a> 에 대해 알아보도록 하자.  

* * *  

## 1. Data Transformation Preview  

🧩 Data Transformation은 <a>데이터의 전체 attribute를 새로운 값으로 변경해주는 일종의 함수</a> 를 의미한다. 즉, 기존의 값을 새로운 값으로 바꿔준다는 것에 그 의미가 있다.  

🧩 Data Transformation을 위한 method로는 다음과 같은 방법들이 있다.  


- <b>1.  </b><a>Smoothing</a><br>  
    - 데이터의 noise 제거  
    - outlier를 원래 데이터의 분포에 맞게 바꿈.<br>  

- <b>2.  </b><a>Attribute / Feature Construction</a><br>  
    - 기존의 attribute 를 가지고 새로운 attribute를 생성<br>  

- <b>3.  </b><a>Aggregation</a><br>  
    - 데이터를 다양한 범주로 나눠서 요약함  
    - ex) 학과 / 성별 / 혈액형<br>  

- <b>4.  </b><a>Normalization</a><br>  
    - 데이터를 내가 원하는 특정한 specified된 range로 scaling하는 것.<br>  
        - <a>Min-Max Normalization</a> : min-max range  
        - <a>Z-Score Normalization</a> : 표준정규분포화  
        - <a>Normalization by Decimal scaling</a> : 데이터의 최대 자릿수로 scaling<br>  

- <b>5.  </b><a>Discretization</a><br>  
    - 데이터를 컨셉에 따라서 묶어줌  
    - Aggregation과 유사함  
    - ex) 지역을 우편번호에 따라서 나눔<br>  

👉 대략 다섯개의 방법으로 나눠지는데, 이 중에서 주로 사용되는 방법은 <a>Normalization</a> 과 <a>Discretization</a> 이다. 다음 절부터 이 두가지 방법에 대해서 알아보도록 하자🙃🙃.<br>  


## 2. Normalization  

🧩 데이터, 주로 attribute들을 원하는 범위 내에서 정규화한다고 이해하면 될 것 같다.<br>  

* * *  

### 🚩 2.1 Min-Max Normalization  

🧩 데이터를 설명하고자 하는 새로운 최대, 최소 범위를 설정하여 정규화 진행<br>  

🧩 실제 데이터의 range [$min_{A},\; max_{A}$] 와 새로운 range [$new_{-}min_{A},\; new_{-}max_{A}$] 에 대해서<br>  

<center>Normalization하려는 값 $v$에 대해서</center><br>  

<center>$v' = \frac{v-min_{A}}{max_{A}-min_{A}}\,(new_{-}max_{A}-new_{-}min_{A})\,+\,new_{-}min_{A}$</center><br>  

👉 예제를 한번 살펴보자.<br>  

- 원본 value $v= 73600$  
- 실제 데이터 range = $[12000, 98000]$  
- 새로운 range = $[0.0, 1.0]$<br>  

$v' = \frac{73600-12000}{98000-12000}\,(1.0-0.0)\,+\,(0.0) = 0.716$<br>  

🧩 이렇게 Min-Max Normalization을 사용해서 원본 데이터에서는 정확히 알 수 없었던 데이터의 위치나 분포를 간단하게 알 수 있다. 데이터를 상대적인 위치로 표현하고자 할때 특히 유용한 방법이다. 따라서 대부분의 경우에 데이터를 표현하려는 범위를 0과 1 사이로 잡고 normalize한다.<br>  

* * *  

### 🚩 2.2 Z-Score Normalization  

🧩 통계학을 이미 알고 있는 사람이라면 아마 익숙할 것이라 생각한다. <a>Z-Score</a> 는 평균이 0이고 표준편차가 1인 정규화된 분포로써 가우시안 분포라고도 한다. 대부분의 표본정규분포를 z-score에서 구하기 때문에, 표본의 평균과 표준편차만으로 데이터를 정규화할 수 있으면서도 익숙한 방법이다.<br>  


<center>표본평균 $μ$와 표준편차 $σ$에 대해서</center><br>  

<center>$v'=\frac{v-μ_{A}}{σ_{A}}=\frac{v-표본평균}{표준편차}$</center><br>  

👉 예제를 한번 살펴보자.<br>  

- $μ=54000$  
- $σ=16000$  
- $v=73600$<br>  

$v'=\frac{73600-54000}{16000}=1.225$<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/183293789-f66b0e9e-9d15-4644-9208-2949e174b2fb.jpg" width="600" /></p><br> 

🧩 이렇게 정규화한 값을 위와 같이 평균이 0이고 표준편차가 1인 표준정규분포표에서 찾음으로써 이 데이터의 위치가 어느정도인지, 그 확률은 얼마인지 알 수 있다.<br>  

* * *  

### 🚩 2.3 Normalization by Decimal scaling  

🧩 위의 두 방법에 비해서 처음에 들었을 때 굉장히 생소했던 정규화 방법이었다. 하지만 그 개념은 생각보다 훨씬 간단했다. 그냥 데이터들을 그 중에 <a>$10^{maximum\;decimal}$</a>로 나눠 정규화하는 방법이다. 이렇게 개념을 설명하기보다 예제를 한번 보면 이해가 바로 될 것 같다.<br>  


<center>$Deciaml\;Scaling\;for\;\;\;data\;[2000,4000,6000,10000,64000]$</center><br>  

👉 위의 데이터를 보면 알겠지만 각 데이터의 자릿수가 $[4,4,4,5,5]$ 이다. 그러면 이제 우리는 각 데이터를 $10^{maximum\;decimal}$인 $10^{5}$으로 나눠주기만 하면 된다.<br>  

따라서 정규화 후 데이터는 아래와 같다.<br>  

<center>$[0.02,0.04,0.06,0.1,0.64]$</center><br>  

## 3. Discretization  

🧩 앞서 살펴본 Normalization이 데이터를 정규화해서 새로운 범위로 표현했다면 <a>Discretization</a>은 데이터를 몇가지 범위로 분류하는  방법이다. 우리가 이때까지 공부한 데이터의 자료형은 크게 Nominal, Ordinal, Numeric으로 나눠지는데, Discretization은 이 중에서 Numeric 데이터를 분류하기 위해서 사용한다.  

🧩 정리하자면 Discretization은 <a>Continuous attribute</a>의 범위를 구간으로 분할해서 각 데이터에 범위를 기준으로 <a>Label</a>을 부여한다. 이후 각 Label을 사용해서 실제 데이터 값을 표현한다.  

🧩 Discretization을 위한 방법들은 다음과 같다.<br>  

- <a>Binning</a> : unsupervised  
- <a>Histogram analysis</a> : unsupervised   
- <a>Clustering analysis</a> : unsupervised  
- <a>Classification (Decision Tree)</a> : supervised  
- <a>Correlation</a> : unsupervised<br>  

👉 Clustering과 Classification, Correlation에 대해서는 나중에 훠어어얼씬 더 비중있게 다룰 것이기 때문에 넘기고 이번 포스팅에서는 Binning에 대해서만 알아볼 생각이다.<br>  

* * *  
### 🚩 3.1. Binning  

🧩 Binning은 Discretization의 가장 대표적인 방법으로, 데이터를 범위로 분류하여 각각에 Label을 붙여 표현하는 방법이다. 아무래도 전반적인 데이터의 구간을 신경써야 할 것이기 때문에 극값의 영향을 많이 받는다는 특징이 있다.<br>  

🧩 Binning의 방법은 크게 두 가지로 분류된다.  

- <a>Equal-width</a> (Equal-distance) partitioning : 각 Bin(구간)의 간격이 같도록 설정<br>  
- <a>Equal-depth</a> (Equal-frequency) partitioning : 각 Bin 마다 같은 개수의 데이터가 들어가도록 설정<br>  

🧩 Binning의 특징을 정리하면 다음과 같다.  

- label의 개수를 줄임으로써 데이터의 사이즈를 줄일 수 있다.  
- Equal-width 의 경우에는 극값의 영향을 특히 많이 받기 때문에 이를 보완하기 위해 나온 방법이 Equal-depth 이다.  
- 데이터의 scaling에 좋다.  
- 하지만 Binning을 가지고 데이터를 정확하게 구분지을 수는 없다.<br>  

👉 예제를 한번 살펴보도록 하자🙃.<br>  

$data = [4,8,9,15,21,21,24,25,26,28,29,34]$<br>  

<b>1. Equal-depth (Equal-frequency) partitioning</b><br>  

- 각 Bin 마다 같은 개수의 데이터가 들어가도록 설정<br>  
    - Bin 1 : [4,8,9,15]  
    - Bin 2 : [21,21,24,25]  
    - Bin 3 : [26,28,29,34]<br>  

<b>2. Smoothing by bin means</b><br>  

- Equal-depth의 결과 각 Bin에 대해서 평균을 취함<br> 
    - Bin 1 : [9,9,9,9]  
    - Bin 2 : [23,23,23,23]  
    - Bin 3 : [29,29,29,29]<br>  

<b>3. Smoothing by bin boundaries</b><br>  

- Equal-depth의 결과 각 값을 각 Bin의 더 가까운 양끝 boundary로 보냄<br>  
    - Bin 1 : [4,4,4,15]  
    - Bin 2 : [21,21,25,25]  
    - Bin 3 : [26,26,26,34]<br>  

* * *  

🧩 이번 포스팅까지 해서 드디어<br>  

- Data Cleaning  
- Data Integration  
- Data Reduction  
- Dimensionality Reduction  
- Data Transformation<br>  

까지에 이르는 Preprocessing에 대해서 모두 알아보았다. 양도 많고 개념도 많아서 어떤 상황에 정확히 뭘 사용할지 헷갈리기도 하지만, 전반적인 목적은 데이터를 우리가 원하는 형태로 전처리한다는 것을 주로 알고 있으면 좋을 것 같다. 각각이 독립적이라기보다는 데이터를 깔끔하게 만들기 위해서 복합적으로 사용한다는 느낌이 중요하다고 생각한다🙃🙃.  

🧩 다음 포스팅에서는 Preprocessing에 대해서 깔끔하게 흝어보기로 하자🏃‍♂️🏃‍♂️.  

* * *  

<div style="text-align: left">💡위 포스팅은 한국외국어대학교 바이오메디컬공학부 고윤희 교수님의 [생명정보학을 위한 데이터마이닝] 강의 내용을 바탕으로 함을 밝힙니다.</div>
---
title : "🧩 Data Mining (14) - Preprocessing_7 : Data Reduction - Nonparametric"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Preprocessing, Reduction, Nonparametric]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-07-15
last_modified_at: 2022-07-15 
---  
  
* * *  

🧩 앞의 두 포스팅을 통해서 데이터의 object를 줄이는 Numerosity reduction 중에서 파라미터를 사용하는 방법들을 살펴보았다. 이번에는 파라미터를 사용하지 않는 방법을 배워보도록 하자.  

* * *  
## 1. Nonparametric Method 1 : Histogram Analysis  

🧩 먼저 <a>Histogram Analysis</a>에 대해서 알아보자. 히스토그램이라면 가장 먼저 떠올리는 것이 우리가 중고들학교때 배운 히스토그램 그래프일 것이다. 변량을 각 계급으로 나눠서 도수를 표현 하는 것을 히스토그램이라고 배웠을 텐데, 여기서 배울 Histogram Analysis도 똑같다. 앞으로의 설명을 위해서 각 계급을 bucket이라고 부를 것이다.<br>  

- <b>📝 Histogram Analysis</b><br>  
    - 데이터를 bucket으로 나눠서 각각의 bucket에 보관하는 방법  
    - 데이터를 나누는 방법이기 때문에 <a>Partitioning Rules</a>라고 하며, Binning 이라고도 함<br>  
        - <b>Equal-Width</b> : 각 bucket의 range를 모두 같게 설정해서 partition 하는 방법. 극값의 영향을 많이 받음<br>  
        - <b>Equal-Frequency</b> : 각 bucket에 들어가는 데이터가 같도록 bucket을 설정하는 방법 (= equal depth)<br>  

👉 위에서 업급한 것처럼 Histogram Analtsis는 두 가지의 방법으로 나눠진다. 나도 배울 때 그랬지만, 저 설명만을 가지고는 직관적인 이해가 어렵다. 쉬운 이해를 위해 그림을 한번 살펴보도록 하자.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/179148064-357ab521-9615-4cbf-a1e4-f045e8cec6e1.png" width="600" /></p>  

- <a><b>Equal Width</b></a>는 일단 bucket의 range를 같은 사이즈로 나눠두고, 그에 맞취 도수를 구하는 방법이다. 데이터의 분포를 고려하지 않고 bucket을 나누기 때문에 극댓값이나 극솟값의 영향을 많이 받을 수 밖에 없다.<br>  
- 반면 <a><b>Equal Frequency</b></a>는 우선적으로 각 bucket에 들어가는 도수의 개수가 같도록 미리 나눈 후에, 마지막에 bucket의 range를 정하는 것이라고 보면 될 것 같다. Equal Width 방법의 극값에 의한 영향을 보완하기 위해 만들어진 개념이다.  

* * *  

## 2. Nonparametric Method 2 : Clustering  

🧩 이번에는 Clustering에 대해 알아보자. 사실 clustering은 데이터마이닝에 있어서 정말 중요한 내용이기 때문에, 거의 반 학기 정도를 clustering에 대해서 배웠던 것 같다. 뒤에 이에 대해서 정말 자세히 다룰 것이기 때문에, 이번에는 정말 간단한 개념만 이해하고 가도록 하자.  

- <b>📝 Clustering</b><br>  
    - 데이터를 <a>비슷한 애들끼리</a> 묶어서 나누고 representation을 저장함. <a>군집화</a>라고도 함.  
    - 데이터가 미리 클러스터링 되어 있거나 나누기 좋은 데이터라면 굉장히 효율적인 방법이지만, 군데군데 흩어진 데이터라면 쉽지 않음  
    - 이를 위한 다양한 방법이 있음.  

* * *  

## 3. Nonparametric Method 3 : Sampling  

- <b>📝 Sampling</b><br>  
    - 전체 데이터 N을 대표하는 작은 n개의 sample을 얻는 것  
    - Choose a representive subset of the data : 대표성을 가지는 sample을 얻음<br>    
    - Types of Sampling  
        - Simple random sampling : 샘플링을 위해 같은 확률로 데이터를 선택함  
        - Sampling without replacement : 비복원추출  
        - Sampling with replacement : 복원추출  
        - Stratified Sampling : partition이 속한 집단의 특성에 맞게 샘플링 진행 (ex. class 개수의 비율을 유지)<br>  

  

* * *  

🧩 이번 포스팅까지 해서 데이터의 object 수를 줄여 dimension을 감소시키는 법을 배워보았다. 파라미터를 사용하는 방법과 파라미터를 사용하지 않는 방법으로 구분된다는 차이점만 이해하면 좋을 것 같다. 마지막으로 두 방법의 차이점을 간단히 알아보고 이번 포스팅을 마무리해야겠다😃😃.<br>  

- <b>Parametric / Nonparameric 비교</b><br>  
    - <a>Parametric Approach</a>  
        - Assumption ⭕, Parameter ⭕  
        - Linear Regression  
        - Nonlinear Regression  
        - 파라미터 업데이트를 통한 모델 피팅 가능  
        - 하지만 모델의 가정에 의한 영향을 많이 받음<br>  

    - <a>Nonparametric Approach</a>  
        - Assumption ❌, Parameter ❌  
        - Histogram  
        - Clustering  
        - Sampling  
        - 모델에 대한 가정을 하지 않음<br>  

🧩 다음 포스팅부터는 Dimension을 줄이는 Dimensionality Reduction에 대해 알아보자🏃‍♂️🏃‍♂️.  

* * *  
<div style="text-align: left">💡위 포스팅은 한국외국어대학교 바이오메디컬공학부 고윤희 교수님의 [생명정보학을 위한 데이터마이닝] 강의 내용을 바탕으로 함을 밝힙니다.</div>
---
title : "🧩 Data Mining (20) - Preprocessing_13 : Review"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Preprocessing]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-08-08
last_modified_at: 2022-08-08 
---  
* * *  

🧩 이때까지 정말 많은 Data Preprocessing 방법에 대해 알아보았다. 이번 포스팅에서 그 개념들을 간단하게 살펴보는 것으로 Preprocessing을 마무리짓도록 하자.  

* * *  

## 1. Data Cleaning  

- Missing Data / Noisy Data / Outlier / Inconsistence 등을 다뤄 데이터를 깨끗이 <a>정리.</a><br>  

## 2. Data Integration  

- 여러 데이터나 데이터베이스를 <a>통합.</a>  
- <a>Redundancy</a> 조절 필요 : 상관관계 분석 / 공분산 분석<br>  

- <A>Categorical Data</a> - correlation analysis : chi-square test<br>  

- <a>Numerical Data</a> - variance analysis  
    - covariance ($σ_{12}$) : range [$-∞, +∞$]  
    - correlation ($ρ_{12}$) : range [$-1,1$]<br>  

## 3. Data Reduction  

- 지나치게 복잡한 데이터 분석에는 많은 시간과 비용이 들기에 불필요한 attribute를 <a>제거</a>해야 함.  
- 단, Reduction 전후의 결과는 비슷하게 유지되어야 함.<br>  

- <a>Attribute Reduction</a> (Demensionality Reduction) - Subset selection, PCA<br>  

- <a>Observation Reduction</a> (Numerosity Reduction)<br>  
    - Parametric model : Regression  
    - Non-parametric model : histogram / Clustering / Sampling<br>  

- <a>Data Compression</a> - String Compression / Audio-Video Compression<br>  

## 4. Dimensionality Reduction  
  
- Random Variables의 수를 줄여서 주요한 Variables를 만드는 것  
- Irrelevant attribute 제거<br>  

- <a>Feature Selection</a><br>  
    - Best subset selection  
    - Forward stepwise selection  
    - Backward stepwise selection<br>  

- <a>Feature Extraction</a> - PCA<br>  

## 5. Data Transformation  

- 전체 Attribute 값을 새로운 값으로 변경해주는 함수<br>  

- <a>Smoothing</a><br>  
- <a>Attribute / Feature Construction</a><br>  
- <a>Aggregation</a><br>  
- <a>Normalization</a><br>  
    - Min-Max Normalization  
    - Z - score Normalization  
    - Decimal Scaling<br>  
- <a>Discretization</a><br>  
    - Binning  
    - Histogram / Clustering  
    - Classification : Decision Tree  
    - Correlation<br>  

* * *  

🧩 이렇게 정리가 끝났다. 지난 학기에 배우는 동안에는 개념도 많이 헷갈리고, 뭐가 뭔지 정확히 알기도 어려웠던 것 같은데 블로그에 정리를 하면서 나도 몰랐던 개념들을 다시 잡아나가는 기회가 됐던 것 같다. 블로그 포스팅 내용도 꽤나 많았기 때문에, 각 개념들에 대한 블로그 링크를 첨부할 테니 참고하시면 좋을 것 같다😃😃.<br>  

[📝 Preprocessing_1 : Data Cleaning](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-1/)  
[📝 Preprocessing_2 : Data Integration - chi-square test](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-2/)  
[📝 Preprocessing_3 : Data Integration - Numerical Data](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-3/)  
[📝 Preprocessing_4 : Data Reduction - Introduce](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-4/)  
[📝 Preprocessing_5 : Data Reduction - Linear Regression](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-5/)  
[📝 Preprocessing_6 : Data Reduction - Nonlinear Regression](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-6/)  
[📝 Preprocessing_7 : Data Reduction - Nonparametric](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-7/)  
[📝 Preprocessing_8 : Data Reduction - Dimensionality](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-8/)  
[📝 Preprocessing_9 : Data Reduction - Subset Selection](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-9/)  
[📝 Preprocessing_10 : Data Reduction - PCA](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-10/)  
[📝 Preprocessing_11 : Data Reduction - PCA_2](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-11/)  
[📝 Preprocessing_12 : Data Transformation](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-12/)  

🧩 다음 포스팅부터는 pattern analysis에 대해 배워보도록 하자🏃‍♂️🏃‍♂️.  

* * *  

<div style="text-align: left">💡위 포스팅은 한국외국어대학교 바이오메디컬공학부 고윤희 교수님의 [생명정보학을 위한 데이터마이닝] 강의 내용을 바탕으로 함을 밝힙니다.</div>

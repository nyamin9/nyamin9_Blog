---
title : "🧩 Data Mining (16) - Preprocessing_9 : Data Reduction - Subset Selection"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Preprocessing, subset selection, Dimensionality]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-07-23
last_modified_at: 2022-07-23 
---  
  
* * *  

🧩 이번 포스팅부터는 Dimensionality reduction에 대해 자세히 알아볼 것이다. 먼저 <a><b>subset selection</a></b>에 대해서 알아보도록 하자.  
* * *  

## 1. Attribute Subset Selection 개념  

🧩 이번 포스팅에서는 subset selection에 대해서 알아볼 텐데, 그러면 이게 대체 무엇인가부터 대략적으로 알고가는 편이 좋을 것 같다. 이름에서 느껴질 수 있겠지만, <a><b>데이터의 attribute에서 몇가지를 추출해서 그 attribute들로 이뤄진 subset, 즉 부분집합을 찾겠다는 의미이다.</b></a> 이때 선택하는 attribute들은 데이터를 가장 잘 설명할 수 있어야 하며, 원래 데이터에서 중복값을 제거하거나 필요없는 값을 제거하는 과정에서 자연스럽게 원본 데이터의 dimensionality가 줄어든다.  

🧩 그 방법에는 아래와 같은 방법들이 있다.<br>  

- <a>Best Subset Selection</a><br>  
- <a>Stepwise Selection</a>  
    - Forward Stepwise Selection  
    - Backward Stepwise Selection  
    - Heuristic Search<br>  

👉 첫번째로 <a>Best Subset Selection</a>부터 알아보도록 하자🏃‍♂️!!  
* * *  


## 2. Best Subset Selection  

🧩 10개의 attribute를 가지는 데이터가 있다고 생각해보자. 이 데이터에 대한 best subset은 다음과 같이 구해진다.<br>  

<center>1. attribute가 하나도 없는 <a>null model</a> 생성 : $μ_0$</center><br>  
<center>2. k = 1, 2,..., 10 에 대해서 각 k에 대해서 $_{10}C_k$의 모델을 생성함</center><br>  
<center>3. 2의 과정을 통해서 $_{10}C_1 + _{10}C_2+...+_{10}C_10$개의 모델이 생성됨</center><br>  
<center>4. k에 대해서 $_{10}C_k$ 개의 모델에서 제일 좋은 성능을 보이는 모델 $μ_k$을 하나씩 선정</center><br>  
<center>5. 4에서 만들어진 $μ_1, μ_2,...,μ_10$ 중에서 단 하나의 Best Model을 선택함</center><br>  

👉 요약하자면, 원본 데이터에서 가장 좋은 성능을 보이는 subset을 찾기 위해 가능한 모든 attribute 개수 조합을 모두 생성하고 평가하는 과정이다. 위에서는 attribute가 10개인 원본 데이터를 사용했지만, 실제로 우리가 다룰 데이터는 훨씬 거대한 데이터일 것이기 때문에 <a>연산과정이 너무 많다</a>는 단점은 더욱 크게 다가온다. 그래서 이렇게 모든 경우를 하나하나 체크하는 방법이 아닌 다른 방법이 생겨났으며, 이 방법을 바로 <a>Stepwise Selection</a>이라고 한다.  

* * *  

## 3. Stepwise Selection  

🧩 1절에서 언급했듯이, <a>Stepwise Selection</a>은 세가지 종류로 나눠진다. 세가지 방법 모두 기본적인 알고리즘은 비슷하고 모델을 고르는 방향이나 방법만 살짝 다르기 때문에, 첫번째 방법만 확실히 이해하면 나머지 부분들을 이해하는 데에 어려움은 없을 것 같다. 먼저 <a>Forward Stepwise Selection</a>에 대해 알아보도록 하자🙃.<br>  

- <b>1. Forward Stepwise Selection</b><br>  
    - Best Subset Selection과 같이 Null Model부터 시작해서 attribute를 추가해나간다.<br>  
    - Null Model $μ_0$에 한번에 하나의 attribute만을 추가해가면서 model의 성능을 향상시킨다.<br>  
    - 기존의 모델은 그대로 가져가면서 새로운 attribute를 추가하는 것이다.<br>
    - 이때 attribute를 추가하는 과정은 모델의 성능이 향상될 때 까지만 이뤄진다.  만약 추가한 경우 모델의 성능이 저하된다면, 추가하기 전의 모델이 최종 모델이 되는 셈이다.<br>  
  
👉 아래 그림을 보면서 Best Subset Selection과 비교하면 이해에 도움이 될 것이다. 이때 사용한 데이터는 지출과 가정에 관련된 몇가지 attribute를 포함하는 데이터이다.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/180596534-e5f33d66-4b0e-4aaa-86d2-f2e944fa1255.png" width="1000" /></p>  

👉 앞서 언급했듯이 Stepwise Selection은 모델의 성능이 향상되지 않으면 더이상의 선택을 진행하지 않고, 기존에 선택된 attribute들을 고정해둔 상태에서 가져가기 때문에 local optimum에 빠질 수 있다. 따라서 항상 제일 좋은 모델을 보장할 수는 없지만, Best Subset Selection에 비해 연산량이 확연히 줄어들기 때문에 이 방법을 사용하는 경우가 많다.<br>  

🧩 이제 두번째 방법인 <a>Backward Stepwise Selection</a>에 대해 알아보도록 하자.  

- <b>2. Backward Stepwise Selection</b><br>  
    - 앞선 방법들과 달리 Null Model이 아닌 모든 attribute를 가지고 있는 Full Model부터 시작한다.<br>  
    - Full Model에서 가장 영향을 덜 주는 attribute부터 하나씩 제거하면서 모델을 업데이트한다.<br>  
    - 이 경우 역시 모델의 성능이 향상될 때까지만 업데이트가 이뤄진다.<br>  
    - 따라서 Local Optimum에 빠질 수 있다.<br>  

👉 Forward Stepwise Selection과 Backward Stepwise Selection을 비교해보면 알겠지만, 모델을 업데이트할때 attribute를 추가하느냐, 삭제하느냐의 방향성의 차이일 뿐이다. 연산량이 적다는 장점을 가지지만, Local Optimum에 빠질 수 있다는, 어떨게 보면 치명적인 단점을 가지고 있기 때문에 이를 보완하기 위한 방법이 필요했다. 그래서 등장한 방법이 바로 <a><b>Heuristic Search</b></a> 이다.<br>  

- <b>3. Heuristic Search</b><br>  
    - Best combined attribute selection and elimination<br>  
    - Forward와 Backward를 반복하면서 모델을 업데이트<br>  
    - Local Optimum 탈출<br>  

* * *  
🧩 이번 포스팅에서는 dimensionality reduction 중에서도 feature extraction 방법인 <a>Subset Selection</a>에 대해 알아보았다. 데이터마이닝을 공부하면서 하나의 방법이 나오고 그 방법을 보완할 수 있는 방법들이 계속해서 생겨난다는 느낌을 받았다. 어떠한 개념을 공부할 때 그 방법에 대한 수식이나 이론을 아는 것도 중요하지만, 그 개념과 관련된 하나의 스토리를 아는 것이 장기기억에는 더 도움이 될 거라고 생각한다. 이 블로그를 보는 대부분의 분들이 데이터 마이닝에 대한 기초를 알기 위해서라고 생각하는데, 이렇게 스토리텔링에 집중해서 공부하면 많은 개념을 좀 더 효율적으로 이해할 수 있을 것 같다😃😃.  

🧩 다음 포스팅에서는 PCA에 대해서 알아보도록 하자🏃‍♂️🏃‍♂️.  

* * *  
  
<div style="text-align: left">💡위 포스팅은 한국외국어대학교 바이오메디컬공학부 고윤희 교수님의 [생명정보학을 위한 데이터마이닝] 강의 내용을 바탕으로 함을 밝힙니다.</div>
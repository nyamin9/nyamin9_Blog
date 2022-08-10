---
title : "🧩 Data Mining (21) - Pattern_1 : Preview"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Pattern, itemset, support]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-08-10
last_modified_at: 2022-08-10 
---  
* * *  

🧩 이번 포스팅부터는 Dataset에서 Pattern을 찾는 <a>Pattern Discovery</a> 에 대해서 다룰 것이다. 특히 이 부분은 생명정보학 분야에 있어서 꽤나 큰 비중을 차지하고, 데이터마이닝에 관련된 중요한 기법 역시 많이 나오기 때문에 주의깊게 보면 좋을 것 같다 (당연히 양도 많다...😨😨).  

🧩 이번 포스팅에서는 Pattern Discovery에 관련된 기초 개념을 알아보도록 하자.  

* * *  
## 1. Pattern Doscovery 란??  

- <a>Patterns</a> : 하나의 dataset에서 함께 발생하거나 연관관계가 깊은 것들.<br>  
    - ex) 함께 팔린 물건들 / 같이 나타나는 단어들 / 함께 나타나는 sequence<br>  

- <a>Pattern Doscovery</a> : dataset에서 <a>inherent reqularities</a>를 찾는 것. 즉, <a>고유한 규칙</a>을 찾는 것.<br>  

- 데이터마이닝을 위한 기초 작업이라고 할 수 있음.<br>  
    - Association / Correlation / Casuality analysis  
    - Mining Sequential / Structure Patterns  
    - 패턴분석 : 시공간 / 멀티미디어 / 시계열 / 스트림데이터  
    - <a>Classification</a> : pattern based analysis - Discriminative  
    - <a>Cluster analysis</a> : pattern based clustering - subspace<br>  

- 적용가능한 분야 : Market basket / Cross marketing / Catalog design / <a>Biological Sequence</a><br>  

🧩 이렇게 해서 Pattern Discovery의 개념에 대해서 간략하게 알아보았다. 이제는 기본적인 용어들을 살펴보도록 하자.<br>  

## 2. Pattern Doscovery 기초  

### 🚩 2.1. K-itemsets and Support  

- <a>itemset</a> : 하나 이상 itemset의 set  
- <a>K-itemset</a> : K개로 구성된 itemset<br>  

- <a>absolute-support</a><br>  

    - <b>sup{X}</b>.   
    - itemset X의 출현빈도. 얼마나 많이 등장했는가.  
    - Frequency<br>  

- <a>relative-support</a><br>  
    - <b>s{X}</b>.  
    - itemset X를 포함한 transaction의 비율.  
    - $\frac{Sup}{total\;transaction}$<br>  

🧩 정리해보면 <a>absolute-support</a> 는 itemset X의 <a>빈도</a>를 나타내고, <a>relative-suppor</a> 는 itemset X의 <a>비율</a>을 나타낸다. 저 설명만 보고 두 개념에 대한 차이가 바로 느껴지기에는 어려울 거라 생각해서 수업시간에 다룬 예제를 하나 가져와봤다.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/183826511-6b6a3a7b-a6e2-430e-8a6f-5f9537bfe4e6.png" width="700" /></p><br>  

<center>$sup\{Beer\}=3\;\;\;\;,\;\;\;\;s\{Beer\}=3/5=60\%$</center><br>  
<center>$sup\{Diapper\}=4\;\;\;\;,\;\;\;\;s\{Diapper\}=4/5=80\%$</center><br>  
<center>$sup\{Beer,Diapper\}=3\;\;\;\;,\;\;\;\;s\{Beer,Diapper\}=3/5=60\%$</center><br>  
<center>$sup\{Beer,Eggs\}=1\;\;\;\;,\;\;\;\;s\{Beer,Eggs\}=1/5=20%$</center><br>  

🧩 위의 첨부한 표와 걑은 데이터를 마켓에서 구매한 물품에 대한 정보를 담은 데이터라 해서 <a>Transaction DB</a> 라고 한다.<br>  

* * *  

### 🚩 2.2. Frequent Itemsets (Patterns)  

- <a>minsup</a> : 임의로 설정한 relative-support의 <a>Thresholds</a><br>  

- 만약 itemset X 의 relative-support s{X} 가 설정한 <a>minsup</a> 이상이면 X는 <a>Frequent</a>하다고 한다.  

- 즉, Transaction DB에서 함께, 자주 나타나는 K-itemset 을 어떻게 찾아낼 것인가에 대한 개념이다.<br>  


🧩 이 개념 역시 예제를 한번 살펴보도록 하자!!<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/183826511-6b6a3a7b-a6e2-430e-8a6f-5f9537bfe4e6.png" width="700" /></p><br>  

<center>$Let\;\,minsup\;\;σ=50\%$</center><br>  
<center>$s\{Beer\}=60\%\;\;\;,\;\;\;s\{Nuts\}=60\%$</center><br>  
<center>$s\{Diapper\}=80\%\;\;\;,\;\;\;s\{Eggs\}=60\%$</center><br>  
<center>$s\{Milk\}=40\%\;\;\;,\;\;\;s\{Beer,Diapper\}=60\%\;\;\;,\;\;\;s\{Nuts,Diapper\}=40\%$</center><br>  



👉 위의 예시에서 $minsup=50\%$ 이상의 <a>frequent</a> 한 itemset X는 {Beer} {Nuts} {Diapper} {Eggs} {Beer,Diapper} 에 해당한다. 반면 {Milk} 는 $40\%$ 로 $minsup$ 보다 작기 때문에 <a>frequent</a> 하지 않다. 여기서 주의깊게 봐야할 점이 있는데, 2-itemset {Beer,Diapper} 가 frequent 하다는 것은 1-itemset {Beer}{Diapper} 각각이 frequent하다는 것도 의미한다. 따라서 2-itemset의 frequent 를 판단함으로써 각 sub itemset의 frequent 역시 판단할 수 있다🙃🙃. 위의 예시에서 3개의 item 이 두 개 이상의 transaction에서 나오는 경우는 없기 때문에 2-itemset까지만 구해주었다.<br>  

* * *  


### 🚩 2.3. Association Rule Mining  

🧩 Association Rule Mining 에 대해서 알아보기 전에 알아야 할 개념이 하나 있다. 이 친구 먼저 슬쩍 살펴보고 가도록 하자.<br>  

📝 <b>Support</b><br>  
- transaction 이 $X\cup{Y}$ 를 contain 할 확률. 즉, $X,Y$ 두 itemset을 모두 포함할 확률.<br>  
- ex) $s\{Beer,Diapper\}=60\%$<br>  

📝 <b>Confidence</b><br>  
- conditional probability : $X\cup{Y}$ 에 대한 조건부확률<br>  
- $c=sup(X\cup{Y})/sup(X)$<br>  
- confidence 계산을 위해 사용하는 support는 <a>absolute-support</a>임에 유의.<br>  


- 표현은 $X\rightarrow{Y}(support,confidence)$ 로 한다.<br>  
    - $X\rightarrow{Y}(s,c) : c=sup(X\cup{Y})/sup(X)$<br>  
    - $Y\rightarrow{X}(s,c) : c=sup(X\cup{Y})/sup(Y)$<br>  
    - $X\rightarrow{Y}(s,c)$ 에서 화살표의 시작 부분에 있는 itemset X가 confidence의 조건을 의미한다.<br>  

🧩 이렇게 support, confidence 라는 개념을 알아보았다. 이제는 Association Rule Mining을 알아보도록 하자🙄.<br>  

🧩 <a>Association Rule Mining</a> 에서는 두 개의 임계치를 사용한다. 아까 사용했던 <a>minsup</a>과 confidence에 대한 임계치인 <a>minconf</a> 이다. 그 목적은 minsup과 minconf를 만족하는 연관성을 파악하는 것이며, 최종적으로 그 연관성을 나타내는 모든 rule을 찾아야 한다.<br>  

📝 <b>Association Rule Mining</b><br>  

- 두 개의 임계치 : minsup, minconf 사용  
- 함께 등장하는 itemset 간의 연관성을 파악해야 하므로 2-itemset이 존재해야 한다.<br>  

- Find all rules : $X\rightarrow{Y}(s,c)\;\;that\;\;s\geq{minsup}\;\;and\;\;c\geq{minconf}$<br>  

🧩 위에서 사용한 Transaction Data를 가지고 Association Rule을 찾아보자.<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/183826511-6b6a3a7b-a6e2-430e-8a6f-5f9537bfe4e6.png" width="700" /></p><br>  

우선 minsup을 만족하는 itemset을 먼저 찾아보도록 하자.<br>  

<center>$Let\;\,minsup\;\;σ=50\%$</center><br>  
<center>$s\{Beer\}=60\%\;\;\;,\;\;\;s\{Nuts\}=60\%$</center><br>  
<center>$s\{Diapper\}=80\%\;\;\;,\;\;\;s\{Eggs\}=60\%$</center><br>  
<center>$s\{Milk\}=40\%\;\;\;,\;\;\;s\{Beer,Diapper\}=60\%\;\;\;,\;\;\;s\{Nuts,Diapper\}=40\%$</center><br>  

이때 $minsup-50\%$ 이상인 itemset은 {Beer} {Nuts} {Diapper} {Eggs} {Beer,Diapper} 이다.<br>   

minsup을 만족하는 itemset을 찾았으니 이번에는 minconf를 만족하는 itemset을 찾아야 한다. 두 임계치를 모두 만족하는 경우가 우리가 찾는 rule이기 때문에, 위에서 찾은 itemset에서 confidence를 계산하면 된다.<br>  

<center>$Let\;\,minconf\;\;σ=50\%$</center><br>
<center>$Beer\rightarrow{Diapper} : c=sup(Beer\cup{Diapper})/sup(Beer)=3/3=1$</center><br>  
<center>$Diapper\rightarrow{Beer} : c=sup(Beer\cup{Diapper})/sup(Diapper)=3/4=0.75$</center><br>  

이렇게 구한 support와 confidence로 Association Rule을 표현하면 아래와 같다.<br>  

<center>$Beer\rightarrow{Diapper}(s,c)=(60\%,100\%)$</center><br>  
<center>$Diapper\rightarrow{Beer}(s,c)=(60\%,75\%)$</center><br>  

🚩 $Beer$가 선행조건인 경우와 $Diapper$가 선행조건인 경우 모두 minconf를 만족하기 때문에, 위의 Transaction Data에서 Association Rule은 다음과 같이 존재한다.  

<center>$Beer\rightarrow{Diapper}\;\;\;\;\;and\;\;\;\;\;Diapper\rightarrow{Beer}$</center><br>  
  

## 3. Summary  
  
🧩 이렇게 해서<br>  

- itemset  
- absolute-support  
- relative-support  
- Frequent Itemsets  
- Confidence  
- Association Rule Mining<br>  

에 대해서 알아보았다.  

🧩 전처리나 Classification, Clustering은 평소에 공부하면서 어느정도 익숙한 느낌이 있었는데, 패턴분석은 지난 학기에 완전 처음 배운 내용이었고 오랜만에 공부하다 보니 많이 헷갈렸던 것 같다. 완전히 새로 배우는(...😨) 느낌이 나서 포스팅하는 데에 정말 많은 시간이 걸렸지만, 이렇게 정리하고 나니 그래도 어느 정도 정리되는 것 같아 좋았다. 앞으로의 패턴분석 내용이 이번 포스팅에서 다룬 개본적인 개념을 바탕으로 진행되기 때문에 나름 꼼꼼하게 정리했는데 어떨지 모르겠다. 아무쪼록 도움이 되면 좋겠다ㅎㅎ🙂🙂.  

* * *  

<div style="text-align: left">💡위 포스팅은 한국외국어대학교 바이오메디컬공학부 고윤희 교수님의 [생명정보학을 위한 데이터마이닝] 강의 내용을 바탕으로 함을 밝힙니다.</div>
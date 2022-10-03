---
title : "🧩 Data Mining (28) - Pattern_8 : Null_Invariant Measure (1)"

categories:
    - Data_mining
tags:
    - [Data, Data Mining, Pattern, itemset, Null Invariant, Kulczynski,  Visualization]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-10-03
last_modified_at: 2022-10-03 
---  
* * *  

🐍 확실히 학기가 진행 중에 있으니 블로그에 신경 쓸 시간이 점점 적어지는 것 같다. 본전공과 부전공, 교양 과목들을 듣고 데이터 분석을 위한 SQL 공부도 병행하고 있어서 데이터마이닝 내용에 대해 정리할 여유가 없다...😥😥. 하지만 전공 수업에서 리눅스도 다루고 있기 때문에 수업 내용을 차근차근 정리하면서 블로그를 좀 더 알차게 만들어봐야겠다.<br>  

🐍 저번 글에서는 support, confidence, lift를 가지고 각 attribute 간의 패턴을 알아보았다. 이번 글에서는 이 수치들이 가질 수 있는 문제들을 해결하기 위한 <b>Null-Invariant Measures</b>를 사용하여 패턴을 분석할 것이다.<br>  

🐍 코드 진행의 이해를 위해 이번 글에서 사용할 데이터프레임을 먼저 보도록 하자.  

***

📌 <b>1. pre_tran : 수치형/범주형 attribute가 섞여있던 원래 데이터를 범주형 데이터로 만든 것</b>  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/190163699-df8dfc0b-70a4-4447-ba27-52dc3c1113ef.png" width="1000" /></p><br>  

📌 <b>2. transaction : pre_tran을 사용하여 만든 최종 트랜잭션 데이터 - Boolean 표현형</b>  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/190164777-82916228-210e-4990-9c4b-c32433538ad1.png" width="1500" /></p>  

***  

## 1. Null-Invariant Measures 개념  

🐍 transaction dataframe에서 Null data의 개수가 많은 경우를 방지하기 위해서 Null Invariant한 metric 사용<br>  

🐍 Jaccard, kulczynski, IR, chi-square, p-value 사용<br>  

- <b>Jaccard</b> : 교집합/합집합. 두 집합이 동일하면 1, 공통의 원소가 하나도 없으면 0  
- <b>kulczynski</b> : (0.5) * ((교집합/X) + (교집합/Y)). 두 집합이 동일하면 1, 공통의 원소가 하나도 없으면 0  
  - 0.5를 기준으로 두 집합의 관계가 negative인지 positive 인지 알 수 있음.  
- <b>IR</b> : \|X-Y\| / 합집합. 데이터의 분포 형태를 파악하는 데 사용.  
- <b>chi-square</b> : 데이터의 연관관계 분석. 클수록 연관성이 깊은 집합임.  
- <b>p-value</b> : 유의확률을 제공해서 대립가설을 채택할 수 있는지 판단가능.  
  
🐍 일반적으로 chi-square가 크고, kulczynski가 작으면 negative하다고 말할 수 있음.<br>  

🐍 예를 들어, kulczynski가 0.1 이고 IR이 0.98, chi-square가 111 정도로 나타나면 두 집합의 관계는 negative하며, 데이터의 분포가 불균형적이라는 것을 의미함.<br>  

***  

## 2. chi-square 계산  

```py
# chi-square 계산(original cardio dataframe의 attribute 기준)
# scipy.stats의 chi2_contingency를 통해서 contingency table 생성.
# contingency table을 바탕으로 chi-square와 p-value 계산.
pre_tran_2 = pre_tran.drop('cardio', axis = 1)
chi_list_origin = pd.DataFrame()

from scipy.stats import chi2_contingency
for i in range(len(pre_tran_2.columns)):
    f=pre_tran_2.columns[i]
    contigency = pd.crosstab(pre_tran_2[f],pre_tran['cardio'])
    chi, p, dof, expected = chi2_contingency(contigency)
    chi_list_origin = chi_list_origin.append((pd.DataFrame({'chi' :chi, 'p-value':p}, index = [pre_tran_2.columns[i]+" & cardio"])))
chi_list_origin = chi_list_origin.sort_values('chi', ascending = False)

chi_list_origin
```  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/192100699-324e4a52-7e83-4ff5-8141-e9f6330b6646.png" width="300" /></p><br>  

📌 위의 데이터프레임처럼 각 original dataframe의 attribute와 cardio 간의 chi-square 값과 p-value 값이 구해진다. 이렇게 수치만으로 비교하면 번거로우니까 한번 시각화해서 살펴보도록 하자.<br>  

```py
# Category Data 기준 Attribute의 Cardio와의 chi-square 연산 결과 시각화
fig = go.Figure()

fig.add_trace(
    go.Scatter(
    x = chi_list_origin.index, y = chi_list_origin['chi'], mode = 'markers+lines+text',
    text = chi_list_origin['chi'].round(3), textposition = 'top right', textfont_size = 15))

fig.update_layout(
    {
        'title' : {'text':'Attribute-Cardio 별 Chi-Square 값', 'font':{'size' : 25}},
        'xaxis' : {'showticklabels':True, 'tickfont' : {'size' : 15}},
        'template' : 'plotly_white'
    })

fig.show()
```  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/171838919-03db5f46-20a9-4166-b92c-3a87d244365b.png" width="1800" /></p><br>  

***  

🐍 이렇게 해서 별로 길지 않은 코딩을 통해 간단하게 chi-square 값과 p-value를 구할 수 있었다. 하지만 위의 1절에서 개념을 살펴볼 때 보았듯이 chi-square 값만 가지고 이들간의 관계를 단정지을 수는 없다. 따라서 이 값들 뿐만 아니라 다른 Null-invariant measure들까지 사용해서 복합적으로 분석할 것이다.<br>  

🐍 다음 글에서는 이러한 measure 로부터 구해진 값들을 가지고 실제 데이터프레임을 만들어보고 시각화 한 후 분석까지 진행할 것이다😊😊. 

***
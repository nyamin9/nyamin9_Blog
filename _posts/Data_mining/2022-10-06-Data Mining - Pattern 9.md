---
title : "🧩 Data Mining (29) - Pattern_9 : Project_Null Invariant Measure (2)"

categories:
    - Data_mining
tags:
    - [Data, Data Mining, Pattern, itemset, Null Invariant, Kulczynski,  Visualization]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-10-06
last_modified_at: 2022-10-06 
---  
* * *  

🐍 저번 글에 이어 여러 가지 Null invariant measure들을 통해 attribute 간의 관계를 알아보도록 하자.<br>    

***  

## 1. Null Invariant Measure 데이터프레임 생성  

📌 <b>chi-square, p-value</b> 계산  

```py
# chi-square 계산(transaction dataframe 기준 : 각 attribute의 category)
# scipy.stats의 chi2_contingency를 통해서 contingency table 생성.
# contingency table을 바탕으로 chi-square와 p-value 계산.
chi_list = pd.DataFrame()
from scipy.stats import chi2_contingency
for i in range(len(transaction.columns)):
    f=transaction.columns[i]
    contigency = pd.crosstab(transaction[f],transaction['Cardio'])
    chi, p, dof, expected = chi2_contingency(contigency)
    chi_list = chi_list.append((pd.DataFrame({'chi' :chi, 'p-value':p}, index = [transaction.columns[i]+" & cardio"])))
```  

📌 <b>support 계산</b>  

```py
# support 계산 함수
# transaction data와 item을 parameter로 받음
# item이 list 형태면 그대로 item을 반환하며, list가 아니면 list 형태로 바꿔서 items_list로 반환함 - sum()연산
# transaction data에서 item_list의 attribute를 받아 column기준 sum 연산 수행. 
# 변수 a : 위의 sum 연산결과가 items_list의 길이와 같은 row의 개수, 즉 해당하는 items_list의 요소를 모두 가지고 있는 row의 개수를 sum()
# 이를 전체 transaction 수(변수 b)로 나눠서 해당 item 집합이 발생한 확률을 구함.
def support(transaction, item): 
    items_list = item if isinstance(item,list) else list(item)
    a = np.sum(transaction.loc[:,items_list].sum(axis=1)==len(items_list)) 
    b = transaction.loc[:,items_list].shape[0]
    return a/b
```  

📌 <b>Jaccard, Kulczynski, IR 계산</b>  

```py
# 위에서 만든 support 함수를 사용해서 집합 X, 집합 Y, 교집합의 support를 구해서 metric 공식에 대입.
# 얻은 결과값을 dataframe형태로 변환
Null_inv = pd.DataFrame()
for i in range(len(transaction.columns)):
    rslt01 = support(transaction, [transaction.columns[i]])
    rslt02 = support(transaction, ['Cardio'])
    rslt03 = support(transaction, (transaction.columns[i],'Cardio'))
    
    jacc = rslt03 / (rslt01+rslt02-rslt03)
    kulc = (0.5)*((rslt03/rslt01) + (rslt03/rslt02)) 
    ir = abs((rslt01 - rslt02)) / (rslt01+rslt02-rslt03)
    Null_inv = Null_inv.append((pd.DataFrame({'Jaccard' :jacc, 'kulczynski' :kulc, 'IR' : ir}, index = [transaction.columns[i]+" & cardio"])))
```  

📌 데이터프레임 생성  

```py
# chi-square와 p-value, jaccard, kulczynski, IR을 하나의 데이터프레임으로 통합 - Null_inv
Null_inv = pd.merge(Null_inv, chi_list, how = 'outer', left_index=True, right_index=True)
Null_inv = Null_inv.drop(['Cardio & cardio', 'No_cardio & cardio'], axis = 0)

# kulczynski를 기준으로 큰 순서부터 나열
Null_inv = Null_inv.sort_values('kulczynski', ascending = False)
Null_inv
```  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/192140866-a8b850c5-4b6a-49ab-ae05-2fcc5190e5cb.png" width="600" /></p><br>  

🐍 이렇게 해서 최종 값들을 모두 구했는데, 숫자도 너무 복잡하고 그 크기를 비교하기도 힘들다. 따라서 이 중에서 가장 데이터를 잘 표현하기로 알려진 kulczynski와 IR을 시각화해서 attribute 간의 관계를 분석할 것이다.<br>  

***  

## 2. 시각화  

```py
# 시각화를 위한 plotly library 임포트
import plotly.graph_objects as go
import plotly.offline as pyo
pyo.init_notebook_mode()

# Transaction Data의 Attribute-Cardio 별 Kulczynski / IR 값 시각화
fig = go.Figure()

fig.add_trace(
    go.Scatter(
    x = Null_inv.index, y = Null_inv['IR'], mode = 'markers+lines+text', name = 'IR'))
    
fig.add_trace(
    go.Scatter(
    x = Null_inv.index, y = Null_inv['kulczynski'], mode = 'markers+lines+text', name = 'Kulczynski'))
    
fig.update_layout(
    {
        'title' : {'text':'Attribute-Cardio 별 Kulczynski / IR 값', 'font':{'size' : 25}},
        'template' : 'plotly_white'
    })
    
fig.add_hline(y=0.5, line_dash="dot",
              line_color = "#ff0000",
              annotation_text="Kulczynski = 0.5", 
              annotation_position="bottom right",
              annotation_font_size=17,
              annotation_font_color="black"
             )
             
fig.show()
```  

<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plotly.com/~nyamin9/60.embed" height="525" width="100%"></iframe>  


***  

## 3. Null-Invariant Measures 결과  

- <span style="background-color:#ffdce0">kulczynski, IR, chi-square 값으로 몇가지 유추가 가능하다.</span>  
  - (1) 30 & cardio : kulczynski = 0.109444, IR = 0.980692, chi-square = 111.024261 이므로 둘의 관계는 negative하며, 두 집합의 분포가 imbalanced 하다.  
  - (2) HBP_SYS & cardio : kulczynski = 0.640039, IR = 0.431196, chi-square = 10586.494635 이므로 둘의 관계는 positive하고, 두 집합의 분포 역시 어느정도 고르다.<br>  
    
- <span style="background-color:#ffdce0">kulczynski의 결과가 0.5를 기준으로 나뉘고, 그에 따른 IR로부터 몇가지 결과를 얻을 수 있다.</span>  
  - 이때 IR의 값이 하나의 categroy가 가지는 값에 대해서 다양하게 나오고 있으므로, 집합들 사이의 분포가 고르지 않은 경우가 많음을 알 수 있음.  
  - <span style="background-color:#ffdce0">따라서 전체 데이터 크기에 대한 분포의 영향(e.x. BMI -> HIGH_OBESITY)을 배제할 수 없기 때문에 kulczynski와 IR 값만으로 attribute를 선택하는 것은 어려움.</span>  
  - 그럼에도 일단 kulczynski와 IR 값으로 선택한 attribute는 다음과 같음.  
  - [ap_hi, ap_lo, gluc, gender, active, age, cholesterol]  
    
- 전체적으로 큰 chi-square값을 보이나, 그에 비해 작은 결과를 나타내는 attribute를 제외하면 남은 attribute는 아래와 같음.  
  - <span style="background-color:#ffdce0">[age, ap_hi, ap_lo, cholesterol, gluc, active, BMI]</span><br>  
  
***  

🐍 이렇게 해서 Null-invariant measure를 통해 데이터의 패턴을 파악해 보았다. 사실 이 값들의 크기를 통해 관계를 파악하는 데에는 절대적인 기준치가 존재하지 않기 때문에 데이터의 attribute들 사이의 값들만 상대평가해서 패턴을 분석하였다.<br>  

🐍 아무래도 상대적인 값들을 통해 그 관게를 비교할 것이기 때문에 아주 정확한 패턴이라고 말하기는 어렵겠지만, 일단은 이렇게 나온 값들과 관계를 가지고 프로젝트를 진행할 것이다.<br>  

* * *  

🧩 이번 포스팅과 지난 세 개의 포스팅을 통해서 프로젝트 진행을 위해 사용한 패턴 분석에 대해서 알아보았다. 혹시나 더 궁금하신 분들을 위해 아래에 지난 링크들을 남겨놓을 테니, 참고하시면 좋을 것 같다😊😊.  

[📝Project 1](https://nyamin9.github.io/data_mining/Data-Mining-Pattern-6/)  
[📝Project 2](https://nyamin9.github.io/data_mining/Data-Mining-Pattern-7/)  
[📝Project 3](https://nyamin9.github.io/data_mining/Data-Mining-Pattern-8/)  

* * *  

🧩 당분간 시험기간이라서 블로그 활동이 좀 더 뜸해질 것 같다...😥 그래도 기존에 공부하던 자료들을 시간이 된다면 틈틈이 올릴 생각이다. 보잘것없는 블로그이지만 읽어주시는 분들꼐 감사의 말씀을 드린다🙇‍♂️🙇‍♂️. 

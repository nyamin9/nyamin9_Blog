---
title : "π Pandas μκ°ν 3 - plotlyμμ forλ¬Έ μ¬μ©νκΈ°"

categories:
    - Pandas_visual
tags:
    - [Pandas, Plotly, Visualization, forloop]

toc : true
toc_sticky : true

date: 2022-03-13
last_modified_at: 2022-03-14
---

* * *

π κ°κ°νλλ μΌνλμ΄λΌκ³  νκΈ° μ΄λΆν° μμ£Ό λ°μλ€!! μ κ³΅κ³Όλͺ©μ λμ΄λκ° μ λ§ 2νλλμλ λΉκ΅ν  μ μκ² μ¬λΌκ°λ€(λ¬Όλ‘  2λλμ κ΅³μ λ΄ λ¨Έλ¦¬λ νλͺ«νκ² μ§λ§...π). λ°°μ΄ κ±΄ κ·Έλ κ·Έλ  λ³΅μ΅νλ €λ μ΅κ΄μ λ€μ΄κ³  μλλ° κ°κ° μ²«μ£ΌλΆν° μμ¬μμ¬νλ€. κ·Έλλ μ§¬μ§¬μ΄ κ³΅λΆν λ΄μ©λ€μ μ΅λν λΈλ‘κ·Έμ μ¬λ €λ³Ό μκ°μ΄λ€.  

π μ€λμ plotlyμμ for loopλ₯Ό μ¬μ©νλ λ²μ μμλ³΄μ.

* * *
## 3.1 forλ¬Έμ μ¬μ©νμ§ μμ plotly
* * *

π λ¨Όμ  λ°μ΄ν°νλ μμ νλ μ μνμ.  

```py
#pandas μν¬νΈ
import pandas as pd

#plotly μν¬νΈ
import plotly.graph_objects as go
import plotly.offline as pyo
pyo.init_notebook_mode()
```  
```py
score_df = pd.DataFrame({'test' : ['score1','score2','score3','score4','score5','score6'],
                         'A' : [95, 100, 90, 88, 92, 94],
                         'B' : [87, 92, 95, 93, 88, 86],
                         'C' : [92, 92, 86, 95, 90, 84],
                         'D' : [78, 80, 82, 86, 80, 82],
                         'E' : [80, 76, 84, 80, 78, 84]})
score_df = score_df.set_index('test')
score_df
```
```
>>
        A	B	C	D	E
test					
score1	95	87	92	78	80
score2	100	92	92	80	76
score3	90	95	86	82	84
score4	88	93	95	86	80
score5	92	88	90	80	78
score6	94	86	84	82	84
```  

νμ A,B,C,D,E μ 6κ°μ μν μ±μ μ λνλΈ λ°μ΄ν°νλ μμ΄λ€.  

π μΌλ¨ for λ¬Έμ μ¬μ©νμ§ μλ μνμμ μκ°νλ₯Ό μ§νν΄λ³΄μ.  

```py
fig = go.Figure()
fig.add_trace(
    go.Scatter(
        x = score_df.index, y = score_df['A'], name = 'A'))

fig.add_trace(
    go.Scatter(
        x = score_df.index, y = score_df['B'], name = 'B'))

fig.add_trace(
    go.Scatter(
        x = score_df.index, y = score_df['C'], name = 'C'))

fig.add_trace(
    go.Scatter(
        x = score_df.index, y = score_df['D'], name = 'D'))

fig.add_trace(
    go.Scatter(
        x = score_df.index, y = score_df['E'], name = 'E'))

fig.show()
```  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/158064657-e01f137e-f104-4297-a661-a9d38a0d1baa.png" width="900" /></p>  

π forλ¬Έμ μ¬μ©νμ§ μλ κ²½μ°μλ <a>fig . add_trace( )</a> λ₯Ό λ€μ―λ² λͺ¨λ νΈμΆν΄μ κ° νμμ μν μ±μ λ€μ κ·Έλ €μ€λ€. μ΄λ κ² λ°μ΄ν°μ μκ° λ§μ§ μμ κ²½μ°μλ κ΅³μ΄ λ°λ³΅λ¬Έμ μ¬μ©νμ§ μμλ ν° λΆλ΄μ΄ μμ§λ§, λ§μ λ°μ΄ν°λ₯Ό λ€λ£¨λ €λ©΄ μμ λ°©λ²λ§μΌλ‘λ μ’ λ¬΄λ¦¬κ° μμ μ μλ€κ³  μκ°νλ€.  

κ·Έλ¬λ©΄ μ΄λ²μλ for λ¬Έμ μ¬μ©ν΄λ³΄μ.  

* * *
## 3.2 forλ¬ΈμΌλ‘ plotly κ·Έλ €λ³΄κΈ°
* * *  

π λ°μ΄ν°λ μμμ λ§λ  score_df λ°μ΄ν°νλ μμ κ·Έλλ‘ μ¬μ©νλ€. 

```py
score_df
```
```
>>
        A	B	C	D	E
test					
score1	95	87	92	78	80
score2	100	92	92	80	76
score3	90	95	86	82	84
score4	88	93	95	86	80
score5	92	88	90	80	78
score6	94	86	84	82	84
```  

π μ΄λ²μλ for λ¬Έμ κ°μ§κ³  μκ°νν΄λ³΄μ!!  

```py
col = len(score_df.columns)

fig = go.Figure()
for i in range(col):
    fig.add_trace(
        go.Scatter(
            x = score_df.index, y = score_df[score_df.columns[i]], name = score_df.columns[i]))

fig.show()
```  
π λ³μ <a>col</a> μ λ°μ΄ν°μ μ΄ κ°μλ₯Ό λ£μ΄μ£Όκ³ , κ·Έ κ°μλ§νΌ <a>forλ¬Έ</a> μ λλ¦¬λ©΄μ <a>fig . add_trace( )</a> λ₯Ό νΈμΆν΄μ€λ€. κ·Έ λ€λΆν°λ λ°μ΄ν°μ μ΄μ μΈλ±μ€λ‘ μ κ·Όν΄μ€μΌλ‘μ¨ xμΆκ³Ό yμΆμ λ°μ΄ν°λ₯Ό μ ν΄μ€λ€.μ΄λ κ² νκ³  λλ©΄ μκ°νλ μλμ κ°μ΄ λνλλ€.  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/158064679-1c647096-0fcb-40d6-84c8-63c6da7d8081.png" width="900" /></p>  

for λ¬Έμ μ¬μ©νμ§ μμ κ²½μ°μ κ°μ κ²°κ³Όλ₯Ό λνλΈλ€.  
* * *
π λΉμ°ν for λ¬Έμ μ¬μ©νλ©΄ μΌμΌμ΄ νΈμΆν΄μ£Όλ κ²λ³΄λ€ μ½λλ₯Ό μ§λ μκ°μ  μΈ‘λ©΄μμ ν¨μ¨μ μ»μ μ μμ§λ§, μμ [λ€λ₯Έ ν¬μ€ν](https://nyamin9.github.io/pandas_practice/practice2-3/)μμλ μΈκΈνλ―μ΄ μ΄ λ°©λ²μ μμΈλ‘ λ³μκ° λ§μ΄ λ°μνλ μμμ΄λ€(λΉμ°ν λ΄κ° μ λͺ¨λ₯΄λ λΆλΆμΌ μλ μλ€. μ¬λ¬κ°μ§ ννλ‘ μλν΄λ³΄λ€κ° μ±κ³΅νλ©΄ μ§ !!νκ³  ν¬μ€νν  μκ°μ΄λ€π.)  

π λ°μ΄ν°λΆμ κ³΅λΆλ₯Ό νλ€λ³΄λ©΄ λλκ³  νμ΄μ¬ κ³΅λΆλ₯Ό νλ κ²μ΄ μλλλΌλ μ΄λ°μ λ° μν© μμμ μμ°μ€λ½κ² μμ©νλ κ² μ‘°κΈμ© μ΅μν΄μ§λ κ² κ°λ€. μ΄λ κ² μ λ κ² κ³΅λΆνλ©΄μ μ€λ ₯μ΄ λμμΌλ©΄ μ’κ² λ€π.

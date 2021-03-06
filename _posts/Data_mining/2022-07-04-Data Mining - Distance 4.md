---
title : "๐งฉ Data Mining (7) - Distance_4 : Cosine ์ ์ฌ๋"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Distance, Document, Cosine]

toc : true
toc_sticky : true
use_math : true

date: 2022-07-04
last_modified_at: 2022-07-04
---  
* * *  
  
๐งฉ Distance Measure ๋ง์ง๋ง ํฌ์คํ์ด๋ค๐. Document Frequency๋ฅผ ์ํ Cosine Similarity์ ๋ํด ์์๋ณด์.  

## 1. Cosine Similarity of two vectors  

๐งฉ <a>Document Frequency</a>๊ฐ ๋ฌด์์ธ์ง ๊ถ๊ธํ  ์ ์์ ํ๋ฐ, ์ ๋ฌธ๊ธฐ์ฌ๋ ์ธํฐ๋ท ๊ธฐ์ฌ๋ฅผ ๊ฐ์ฅ ๋ํ์ ์ธ ์์๋ก ์๊ฐํ๋ฉด ๋  ๊ฒ ๊ฐ๋ค. ์ฐ์๊ธฐ์ฌ์๋ ์ฐ์๊ธฐ์ฌ๋ง์ ์์ฃผ ๋์ค๋ ์ฉ์ด๋ค์ด ์์ ๊ฒ์ด๊ณ , ์คํฌ์ธ  ๊ธฐ์ฌ์๋ ๊ทธ๋ง์ ์์ฃผ ๋ฑ์ฅํ๋ ์ฉ์ด๋ค์ด ์์ ๊ฒ์ด๋ค. ์๋ก ๋ค๋ฅธ ๋ ๊ธฐ์ฌ๋ค ๊ฐ์ similarity๋ฅผ ๊ณ์ฐํด์ ์ ์ฌ์์ ์์๋ณด๋ ๊ฒ์ด <b><a>Cosine Similarity</a></b>์ ๋ชฉ์ ์ด๋ค. ๋ํ ๋จ์ํ ํ์คํธ๋ค์ ์ ์ฌ์ฑ ๋ฟ๋ง ์๋๋ผ ์ ์ ์ฒด์ ๋ํ ๋ถ์๋ ์งํํ  ์ ์๋ measure์ด๊ธฐ ๋๋ฌธ์ Gene feature ํน์ biologic toxonomy๋ฑ์ ๋๋ฉ์ธ์์๋ ์ฌ์ฉํ๋ ์ถ์ธ์ด๋ค.  

๐งฉ ์์๋ถํฐ ์ดํด๋ณด๋๋ก ํ์.  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/177064371-4111bb08-8ad1-4639-a10d-46b8c7864b2a.png" width="600" /></p>  

๐ ์์ ์์์์ ๊ฐ๊ฐ์ Document๋ค์ด ์ ๋ฌธ๊ธฐ์ฌ๋ฅผ ์๋ฏธํ๊ณ , ๊ฐ column๋ค์ด ์ ๋ฌธ๊ธฐ์ฌ์์ ๋์ค๋ ์ฉ์ด๋ค์ ๋น๋๋ฅผ ๋ํ๋ธ๋ค. ์ด์  ์ฐ๋ฆฌ๋ Frequency๋ฅผ ๋ถ์ํ๊ธฐ ์ํด์ ๊ฐ document์ ๋น๋๋ฅผ vector๋ก ํํํ  ๊ฒ์ด๋ค. ๊ฐ๊ฐ์ ๋ฒกํฐ๋ ์๋์ ๊ฐ์ด ํํ๋๋ค.   

<center>$\overrightarrow{d_{1}}=[5,0,3,0,2,0]$</center><br>  
<center>$\overrightarrow{d_{2}}=[3,0,2,0,1,1]$</center><br>  
<center>$\overrightarrow{d_{3}}=[0,7,0,2,1,0]$</center><br>  
<center>$\overrightarrow{d_{4}}=[0,1,0,0,1,2]$</center><br>  

์์ผ๋ก ์ด ๋ฒกํฐ๋ค์ <a>term-frquency vector</a> ๋ผ๊ณ  ๋ถ๋ฅผ ๊ฒ์ด๋ค. ์ด์  ์ด ๋ฒกํฐ๋ค์ ๊ฐ์ง๊ณ  similarity๋ฅผ ๊ตฌํ๊ธฐ ์ํ measure๋ฅผ ์ดํด๋ณด์.  

๐ <b>Cosine Measure</b>  

๋ ๋ฒกํฐ $\overrightarrow{d_{1}}$, $\overrightarrow{d_{2}}$์ ๋ํ์ฌ (๋จ, ๋ ๋ฒกํฐ๋ term-frquency vector)  

<center>$cos(\overrightarrow{d_{1}}, \overrightarrow{d_{2}}) = \frac{\overrightarrow{d_{1}}\cdot\overrightarrow{d_{2}}}{|\overrightarrow{d_{1}}|\times|\overrightarrow{d_{2}}|}$</center><br>  

๐ ๋ฒกํฐ๋ ๋์ค๊ณ , ๋ด์ ๋ ๋์์ ์ผํ๋ณด๋ฉด ๋ณต์กํด๋ณด์ด๋ ์์ด๊ธด ํ์ง๋ง ๊ทธ๋ฅ ๋จ์ํ ๋ด์  ๊ณ์ฐ ์์์ ํ์๋๋ measure์ด๋ค. ๋ด์ ๊ฐ์ ๋ ๋ฒกํฐ์ ํฌ๊ธฐ์ ๊ณฑ์ ๋ ๋ฒกํฐ ์ฌ์ด์ ๊ฐ์ธ ฮธ์ ์ฝ์ฌ์ธ ๊ฐ์ ๊ตฌํด ๊ณฑํด์ฃผ๋ ๊ฒ์ด๊ธฐ ๋๋ฌธ์, ๊ทธ๋ฅ ๊ทธ ์์ ๋๊ฒจ์ฃผ๋ ๊ฒ ๋ฟ์ด๋ค.  

๐ ์ฝ์ฌ์ธ ๊ทธ๋ํ๋ฅผ ์๊ฐํด๋ณด๋ฉด ์ฝ์ฌ์ธ ๊ฐ์ ฮธ๊ฐ ์์์๋ก ์ปค์ง๋ค.  ๋ฐ๋ผ์ cosine similarity ๊น์ธ $cos(\overrightarrow{d_{1}}, \overrightarrow{d_{2}})$ ๊ฐ ์ปค์ง๋ฉด ๋ ๋ฒกํฐ ์ฌ์๊ฐ์ธ ฮธ๊ฐ ์์์ ๋ ๋ฒกํฐ๊ฐ ์๋ก ๊ฐ๊น๋ค๋ ๊ฒ์ ์๋ฏธํ๋ค. ์ ๋ฆฌํ๋ฉด ๋ค์๊ณผ ๊ฐ๋ค.  

- $cos(\overrightarrow{d_{1}}, \overrightarrow{d_{2}})$๊ฐ ํฌ๋ค = ์ฌ์๊ฐ ฮธ๊ฐ ์๋ค = <a>๋ ๋ฒกํฐ๊ฐ ์๋ก ๊ฐ๊น๋ค</a>  

- $cos(\overrightarrow{d_{1}}, \overrightarrow{d_{2}})$๊ฐ ์๋ค = ์ฌ์๊ฐ ฮธ๊ฐ ํฌ๋ค = <a>๋ ๋ฒกํฐ๊ฐ ์๋ก ๋ฉ๋ค</a>  

๐งฉ ์์ ์์์์ ์ง์  cosine similarity๋ฅผ ๊ตฌํด๋ณด๋ ๊ฒ์ผ๋ก ๋๋ด์๐.  

<center>$\overrightarrow{d_{1}}=[5,0,3,0,2,0]$</center><br>  
<center>$\overrightarrow{d_{2}}=[3,0,2,0,1,1]$</center><br>  
<center>$\overrightarrow{d_{3}}=[0,7,0,2,1,0]$</center><br>  
<center>$\overrightarrow{d_{4}}=[0,1,0,0,1,2]$</center><br>  

$cos(\overrightarrow{d_{1}}, \overrightarrow{d_{2}})$ ์ ๋ํด์  

$\overrightarrow{d_{1}}\cdot\overrightarrow{d_{2}} = 15+0+6+0+2+0=23$<br>  
$|\overrightarrow{d_{1}}| = \sqrt{25+0+9+0+4+0} = \sqrt{38}$<br>  
$|\overrightarrow{d_{2}}| = \sqrt{9+0+4+0+1+1} = \sqrt{15}$<br>  
$cos(\overrightarrow{d_{1}}, \overrightarrow{d_{2}})=\frac{23}{\sqrt{38}\times\sqrt{15}} = 0.963$<br>  

- cosine similarity ๊ฐ์ด 1์ ๊ฐ๊น์ด ํฐ ๊ฐ์ ๊ฐ์ง๊ธฐ ๋๋ฌธ์ ๋ ๋ฒกํฐ๋ ์๋ก ๊ฐ๊น๋ค๊ณ  ํ  ์ ์๋ค.  

* * *  

## 2. Distance Measure ์์ฝ  

- <a>Distance Matrix</a>  
- Q-Q plot  
- Scatter plot  
- <a>Categorical Attributes</a> : Simple Matching  
- <a>Binary Attributes</a> : contingency table  
- <a>Numeric Data</a> : Minkowski Distance  
    - Manhattan (1)  
    - Euclidean (2)  
    - Supremum (โ)  
- <a>Document / Term Frequency</a> : Cosine Similarity  

๐งฉ Distance Measure ๊ด๋ จ ๋งํฌ๋ฅผ ์๋์ ์ฒจ๋ถํด๋์์ผ๋ ํ์ํ ์ฌ๋์ ์ฐธ๊ณ ํ๋ฉด ์ ๋ฆฌ์ ๋์์ด ๋  ๊ฒ ๊ฐ๋ค๐.  

* * *

[๐ 1. QQ plot / Scatter plot ๊ด๋ จ ํฌ์คํ](https://nyamin9.github.io/data_mining/DataMining-QQ-plot/)  
[๐ 2. Distance Matrix ๊ด๋ จ ํฌ์คํ](https://nyamin9.github.io/data_mining/Data-Mining-Distance-1/)  
[๐ 3. Categorical / Binary Attributes ๊ด๋ จ ํฌ์คํ](https://nyamin9.github.io/data_mining/Data-Mining-Distance-2/)  
[๐ 4. Numeric Data - Minkowski Distance ๊ด๋ จ ํฌ์คํ](https://nyamin9.github.io/data_mining/Data-Mining-Distance-3/)  

* * *  

๐งฉ ์ด๋ ๊ฒ ํด์ Distance Measure๋ฅผ ๋ชจ๋ ์์๋ณด์๋ค. ์์์ด ๋ณต์กํด๋ณด์ด๋ ๊ฒฝ์ฐ๋ ์๊ณ , ๊ทธ ๊ฐ๋์ด ํท๊ฐ๋ฆฌ๋ ๊ฒฝ์ฐ๋ ์์ง๋ง ์ด๋ค ์๋ฃํ์ ๋ฐ์ดํฐ์ ์ด๋ ํ measure๋ฅผ ์ฌ์ฉํ๋์ง ์๊ณ  ์์ผ๋ฉด distance๋ฅผ ๊ณ์ฐํ๋ ๋ฐ์๋ ์ ํ ์ด๋ ค์์ด ์์ ๊ฒ ๊ฐ๋ค. ๋๋ถ๋ถ์ measure๊ฐ ํ์ด์ฌ์ด๋ R์ ๊ตฌํ๋์ด ์์ผ๋ ๋ง์ด๋ค๐๐ใใ.  

๐งฉ ๋ค์ ํฌ์คํ๋ถํฐ๋ Data Preprocessing์ ์ํ ๋ฐฉ๋ฒ๋ค์ ์์๋ณด์!!  

* * *  
  
<div style="text-align: left">๐ก์ ํฌ์คํ์ ํ๊ตญ์ธ๊ตญ์ด๋ํ๊ต ๋ฐ์ด์ค๋ฉ๋์ปฌ๊ณตํ๋ถ ๊ณ ์คํฌ ๊ต์๋์ [์๋ช์ ๋ณดํ์ ์ํ ๋ฐ์ดํฐ๋ง์ด๋] ๊ฐ์ ๋ด์ฉ์ ๋ฐํ์ผ๋ก ํจ์ ๋ฐํ๋๋ค.</div>

---
title : "๐งฉ Data Mining (5) - Distance_2 : Categorical / Binary"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Distance, Binary, contingency table]

toc : true
toc_sticky : true
use_math : true

date: 2022-07-02
last_modified_at: 2022-07-02
---  
* * *  
  
๐งฉ ์ ๋ฒ ํฌ์คํ์ ํตํด์ object๋ค ๊ฐ์ Distance๋ฅผ ๋ํ๋ด๋ Matrix๋ฅผ ๋ง๋๋ ๋ฒ์ ๋ํด ์์๋ณด์๋ค. ์ด์ ๋ ๋ณธ๊ฒฉ์ ์ผ๋ก Distance measure์ ๋ํด ์์๋ณผํ๋ฐ, ์ด measure๋ค์ feature์ ์๋ฃํ์ ๋ฐ๋ผ ๋ค๋ฅด๊ฒ ์ ์ฉ๋๋ค. ๋จผ์  <a>categorical feature</a>์ <a>binary feature</a>์ ๋ํ measure์ ๋ํด ์์๋ณด๋๋ก ํ์.  
  
* * *  
## 1. Categorical Attributes - Nominal  
  
- <b>Simple Matching</b>  
    - ๋จผ์  ์์๋ณผ ๋ฐฉ๋ฒ์ simple matching์ด๋ผ๋ ๋ฐฉ๋ฒ์ด๋ค. ์ด ๋ฐฉ๋ฒ์ ํตํ object ์ฌ์ด์ distance๋ ์๋์ ๊ฐ์ด ํํ๋๋ค.  
    <center>$d(i,j)=\frac{(p-m)}{p}$</center><br>  
    
    - ์ด๋ $m$์ feature์ ๋ํด ๊ฐ์ ๊ฐ์ ๊ฐ์์ด๊ณ , $p$๋ ์ ์ฒด ๊ฐ์๋ฅผ ์๋ฏธํ๋ค.  
    - ์ฌ์ค ์์ ์์๋ง ๋ณด๊ณ  ์ดํดํ๊ธฐ๊ฐ ์ฝ์ง ์๊ธฐ ๋๋ฌธ์, ์๋ฅผ ํ๋ฒ ๋ณด๋๋ก ํ์.    
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/176986208-14de889e-3996-4c85-aeeb-b8783d5f1784.png" width="350" /></p>  

์์์ student 2์ 3์ Blood Type์ ๊ฐ์ง๋ง Hair Color๊ฐ ๋ค๋ฅด๊ธฐ ๋๋ฌธ์  distance๋ ์๋์ ๊ฐ๋ค.  

<center>$d(s2,s3)=\frac{(2-1)}{2}=\frac{1}{2}$</center><br>  


๋ฐ๋ฉด student 2์ student 4๋ ๋ feature๊ฐ ๋ชจ๋ ๋ค๋ฅด๊ธฐ ๋๋ฌธ์ distacne๋  ๋ค์๊ณผ ๊ฐ๋ค.  

<center>$d(s2,s4)=\frac{(2-0)}{2}=1$</center><br>  


์ด๋ ๊ฒ ํ๋ฉด ๊ฐ๋จํ๊ฒ simple matching ์ ํตํด distance๋ฅผ ๊ตฌํ  ์ ์๋ค.  

      
- <b>Use a large number of binary attributes</b>  
    - ๊ฐ nominal state์ ๋ํด ์๋ก์ด binary attribute๋ฅผ ์์ฑํ๋ ๋ฐฉ๋ฒ์ด๋ค. ์ฆ, categorical ํํ๋ก ์ฃผ์ด์ง ๊ฐ feature๋ค์ binary ํํ๋ก ๋ฐ๊ฟ์ฃผ๊ฒ ๋ค๋ ์๋ฏธ์ด๋ค. ์ด๋ฅผ ์ ์์์ student 1๊ณผ student 2์ ์ ์ฉํ๋ฉด ์๋์ ๊ฐ์ด ๋ฐ๋๋ค. Blodd type A๋ฅผ 0์ผ๋ก, B๋ฅผ 1๋ก ๋ฐ๊ฟ์คฌ์ผ๋ฉฐ, Hair Color Black์ 1๋ก, Brown์ 0์ผ๋ก ๋ฐ๊ฟ ๋ํ๋ด์๋ค.  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/176986217-f579dbbb-adf8-440a-a0db-2f6fdaca02b7.png" width="350" /></p>  

๐ ๊ทธ ํ์ distance๋ฅผ ๊ตฌํ๋ ๋ฐฉ๋ฒ์ simple matching๊ณผ ๊ฐ๋ค.  

<center>$d(i,j)=\frac{(p-m)}{p}$</center><br>  


* * *  


## 2. Categorical Attributes - Ordinal  

์์์ ๋ค๋ฃฌ nominal data์๋ ๋ค๋ฅด๊ฒ ์์๊ฐ ์๋ ์๋ฃํ์ด๋ค.  

๐งฉ ์ด ๋ฐ์ดํฐ์ distance๋ฅผ ๊ตฌํ๋ ๋ฐฉ๋ฒ์ ordinal variables๋ฅผ ๊ทธ๊ฒ์ ์์๋ก ๋ณ๊ฒฝํด์ฃผ๋ ๊ฒ์ธ๋ฐ, ์ด๋ ์๋์ ๊ฐ์ ๋ฐฉ์์ผ๋ก ์ ํด์ง๋ค.  

<center>$feature\;f,\;index\;\,i,\;\;r_{if}โ{1,2,...,M_{if}}\;\;and\;\;r_{if}=\;value\;ranking,\;M_{if}=\;amount$</center><br> 


<center>$Z_{if}=\frac{r_{if}-1}{M_{if}-1}$</center><br>  





๐ ์์๋ง ๋ณด๋ฉด ๋ญ๊ฐ ๋ณต์กํด๋ณด์ด๋๋ฐ, ๊ทธ๋ฅ ๋จ์ํ ์์๋ฅผ ๋งค๊ธด๋ค๊ณ  ์๊ฐํ๋ฉด ํธํ  ๊ฒ ๊ฐ๋ค. ์์๋ฅผ ํ๋ฒ ์ดํด๋ณด๋๋ก ํ์.  
  
freshman 1 / sopomore 2 / junior 3 / senior 4 ์ ๋ํด์ ๊ฐ๊ฐ์ $Z$๊ฐ์ ๋จผ์  ๋ณด๋ฉด,  
$Z_{if}=0\;\;/\;\;\frac{1}{3}\;\;/\;\;\frac{2}{3}\;\;/\;\;1$ ๋ก ๊ณ์ฐ์ด ๋๋ค.  

์ด $Z$๊ฐ์ ๋ฐํ์ผ๋ก ํด์ distance๋ฅผ ๊ตฌํ๊ฒ ๋๋๋ฐ, ๊ทธ ๊ณ์ฐ์ ๋จ์ ๋บผ์ ์ฐ์ฐ์ด๋ค.  

<center>$d(freshman,senior) = 1-0=1$</center><br>  

<center>$d(junior,senior) = 1-\frac{2}{3}=\frac{1}{3}$</center>
  
* * *  
  
  
## 3. Binary Attributes - 0/1  
  
- binary attribute๋ค์ 0๋๋ 1์ ๊ฐ์ ๊ฐ์ง๊ธฐ ๋๋ฌธ์, ์ด๋ฅผ ๊ฐ๋จํ๊ฒ ํฉ์ณ์ ํ๋์ table๋ก ๋ง๋ค ์ ์๋ค. ์ด table์ <b><a>Contingency Table</a></b>์ด๋ผ๊ณ  ํ๋๋ฐ, ๊ทธ ๋ชจ์ต์ ์๋์ ๊ฐ์ด ๋ํ๋๋ค.  
  
๐ <b>Contingency Table</b>  
  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/176982654-de3d2fe3-5240-422e-9faf-9da222173bc6.png" width="600" /></p>  

๐ ๋ object๊ฐ ๋ชจ๋ 1์ธ ๊ฒฝ์ฐ์๋ q, ๋ชจ๋ 0์ด๋ฉด t, (i,j) = (1,0) ์ด๋ฉด s, (0,1) ์ด๋ฉด r๋ก ๊ฐ๊ฐ ๊ทธ ๊ฐ์ด ์ง๊ณ๋๋ค.์์ธกํ  ์ ์๊ฒ ์ง๋ง, distance๋ฅผ ๊ตฌํ ๋๋ ์ฃผ๋ก s์ r์, similarity๋ฅผ ๊ตฌํ  ๋๋ q์ t๋ฅผ ์ฌ์ฉํ๋ค.  

  
โญโญ contingency table์ ์์ด์ ๋ฐ๋์ ๊ณ ๋ คํด์ผ ํ  ์ ์ด ํ๋ ์๋ค. ์ฐ๋ฆฌ๊ฐ binary๋ก ๋ํ๋ด๋ ๋ฐ์ดํฐ๋ ๋ ๊ฐ์ง ๊ฒฝ์ฐ๋ก ๋ชํํ ๋๋ ์ ธ์ผ ํ๋ค. ํ์ง๋ง ์ด๋ฌํ ๊ฒฝ์ฐ๊ฐ ๊ทธ๋ ๊ฒ ๋ง์ด ์กด์ฌํ์ง๋ ์๋๋ฐ, ์ฃผ๋ก ๋ํ๋๋ ๋๋ฉ์ธ์ด ์ง๋ณ์ ์์ฑ / ์์ฑ์ ํ๋จํ๋ ๋๋ฉ์ธ์ด๋ค. ์๋ฅผ ๋ค๋ฉด ์ฝ๋ก๋ ๊ฒ์ฌ ๊ฒฐ๊ณผ๊ฐ ์์ฑ(1)์ด๋ ์์ฑ(0)์ด๋๋ฅผ ๋ค๋ฃจ๋ ๊ฒฝ์ฐ๋ผ ํ  ์ ์๊ฒ ๋ค. ๊ทธ๋ฆฌ๊ณ  ์ง๋ณ ๊ด๋ จ ์กฐ์ฌ์์ ์ฐ๋ฆฌ๊ฐ ๊ด์ฌ์๋ ๋์์ ์์ฑ์ธ ๊ฒฝ์ฐ์ด์ง, ์์ฑ์ธ ๊ฒฝ์ฐ์ผ ๊ฐ๋ฅ์ฑ์ ๊ทธ๋ ๊ฒ ํฌ์ง ์๋ค. ํ์ง๋ง ๋ ์กฐ์ฌ ๋์์ด ๋ชจ๋ ์์ฑ์ธ ๊ฒฝ์ฐ(q)๋ณด๋ค๋ ๋น์ฐํ ์์ฑ(t)์ผ ๊ฐ๋ฅ์ฑ์ด ๋๊ธฐ์, ์์ contingency table์์ q๋ณด๋ค t๊ฐ ์๋ฑํ ํฐ ๊ฐ์ ๊ฐ์ง ๊ฒ์ด๋ค. ์ด๋ ๊ฒ asymmetricํ table์ ๋ํด์๋ ๋น์ฐํ ์ด ๊ฒฝ์ฐ๋ฅผ ๊ณ ๋ คํด์ผ ํ๋คโญโญ.  
  
๐ ์ด์  ๊ฐ๊ฐ์ ๊ฒฝ์ฐ์ ๋ํ distance๋ฅผ ๊ตฌํด๋ณด๋๋ก ํ์.  

๐งฉ Distance measure for <a>symmetric</a> binary variables  
<center>$d(i,j)=\frac{r+s}{q+r+s+t}$</center><br>

  
๐งฉโญDistance measure for <a>asymmetric</a> binary variablesโญ  
<center>$d(i,j)=\frac{r+s}{q+r+s}$</center><br>

  
๐งฉโญSimilarity measure for <a>asymmetric</a> binary variablesโญ  
<center>$Jaccard\;\,coefficient=Sim_{jaccard}(i,j)=\frac{q}{q+r+s}$</center><br>
  
๐งฉ ์์๋ฅผ ํ๋ฒ ์ดํด๋ณด๋๋ก ํ์!!  


<p align="center"><img src="https://user-images.githubusercontent.com/65170165/176986240-c0f486c9-e7d3-4625-abad-3849d8602d60.png" width="600" /></p>  
  
๐ ์ด๋ค ์ง๋ณ์ ๊ด๋ จ๋ 7๊ฐ์ feature๋ฅผ ๊ฐ์ง 3๊ฐ์ object๋ก ๊ตฌ์ฑ๋ ๋ฐ์ดํฐ์์ ํ์ธํ  ์ ์๋ค. ์ด๋ gender๋ symmetricํ ํน์ง์ ๊ฐ์ง๊ณ  ์๊ธฐ ๋๋ฌธ์ ์ด๋ ์ ์ธํ๊ณ  distance๋ฅผ ๊ณ์ฐํด ์ค ๊ฒ์ด๋ค. ๋ํ test์ ๊ฒฐ๊ณผ์์ ๋์ค๋ P๋ 1๋ก, N์ 0์ผ๋ก ๊ธด์ฃผํ๋ค. ์ด๋ฅผ ๋ฐํ์ผ๋ก contingency table์ ๋ง๋ค๋ฉด ์๋์ ๊ฐ๋ค.  
  
<p align="center"><img src="https://user-images.githubusercontent.com/65170165/176984067-0e80896d-d1c4-45bf-ba7c-7315fcdec53c.png" width="600" /></p>  
  
๐งฉ ์์ ๊ณต์์ ๋ฐ๋ผ์ distance๋ฅผ ๊ตฌํด๋ณด์.  

<center>$d(i,j)=\frac{r+s}{q+r+s}$</center><br>  
<center>$d(jack,jim)=\frac{1+1}{1+1+1}=0.67$</center><br>  
<center>$d(jack,mary)=\frac{0+1}{2+0+1}=0.33$</center><br>  
<center>$d(jim,mary)=\frac{1+2}{1+1+2}=0.75$</center><br>



๐งฉ ์ด๋ ๊ฒ ํด์ binary data์ ๋ํ distance measure ์ญ์ ๋ค๋ค๋ดค๋ค. ๊ณ ๋ คํด์ผ ํ  ๊ฒ๋ ์๊ณ , ๊ทธ ๊ฒฝ์ฐ๋ง๋ค ์ ์ฉ๋๋ ๊ณต์๋ ์ด์ง์ฉ ๋ฌ๋ผ์ง์ง๋ง ์๋ก ๋ค๋ฅธ ๊ฒ๋ค๋ก distance๋ฅผ ๊ณ์ฐํ๊ณ  ๊ฐ์ ๊ฒ์ผ๋ก similarity๋ฅผ ๊ฒ์ฐํ๋ค๋ ๊ฒ๋ง ์๊ฐํ๋ฉด ๊ทธ๋ ๊ฒ ์ด๋ ค์ด ๊ฐ๋์ ์๋ ๊ฒ ๊ฐ๋ค.  
  
* * *  
๐งฉ ์ด๋ฒ ํฌ์คํ์์๋ categorical data์ ๋ํ distance measure๋ฅผ ์์๋ณด์๋ค. ์ข๋ฅ๊ฐ ๋ค์ํ๊ณ , ๋ฐ์ดํฐ์ ๋๋ฉ์ธ์ ๋ฐ๋ผ์ ์ ์ฉํ๋ ๋ฒ์ด ๋ค๋ฅด์ง๋ง ์์ ์์๋ค๋ง ์ ์ดํด๋ด๋ ๋๋ฆ ์ค๊ทผํ๊ฒ ๋์ด๊ฐ ์ ์๋ ๋ด์ฉ๋ค์ธ ๊ฒ ๊ฐ๋ค๐. ์์ผ๋ก ๋์ฌ ๋ด์ฉ๋ค์ ๊ธฐ์ด๊ฐ ๋๋ ๋ถ๋ถ๋ค์ด๊ธฐ ๋๋ฌธ์ ๋๋ฆ ์์ธํ ๋ค๋ค๋ณด์๋๋ฐ, ์ถฉ๋ถํ ์ค๋ช์ด ๋์์ผ๋ฉด ์ข๊ฒ ๋ค. ์ด์  ๋ค์ ํฌ์คํ์์๋ Numerical Data์ distance๋ฅผ ๊ตฌํด๋ณด๋๋ก ํ์๐โโ๏ธ๐โโ๏ธ.  
  
  
* * *  
  
<div style="text-align: left">๐ก์ ํฌ์คํ์ ํ๊ตญ์ธ๊ตญ์ด๋ํ๊ต ๋ฐ์ด์ค๋ฉ๋์ปฌ๊ณตํ๋ถ ๊ณ ์คํฌ ๊ต์๋์ [์๋ช์ ๋ณดํ์ ์ํ ๋ฐ์ดํฐ๋ง์ด๋] ๊ฐ์ ๋ด์ฉ์ ๋ฐํ์ผ๋ก ํจ์ ๋ฐํ๋๋ค.</div>

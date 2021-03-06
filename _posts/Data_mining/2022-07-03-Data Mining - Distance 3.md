---
title : "๐งฉ Data Mining (6) - Distance_3 : Minkowski"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Distance, Numerical, Minkowski]

toc : true
toc_sticky : true
use_math : true

date: 2022-07-03
last_modified_at: 2022-07-03
---  
* * *  

๐งฉ ์ ๋ฒ ํฌ์คํ์์๋ categorical data์ ๋ํ distance measure๋ฅผ ์์๋ณด์๋ค. ์ด๋ฒ์๋ <a>Numerical Data</a>๋ฅผ ์ํ measure์ธ <b><a>Minkowski Distance</a></b>๋ฅผ ๋ฐฐ์๋ณด๋๋ก ํ์.  
  
## 1. Basic Minkowski Distance  
  
๐ Minkowski Distance ์ญ์ ๋ object๋ค ์ฌ์ด์ distance๋ฅผ ๊ณ์ฐํ  ๋ ์ฌ์ฉ๋๋ค. ์๋ฅผ ๋ค๋ฉด,<br>  

<p align="center"><img src="https://user-images.githubusercontent.com/65170165/177021852-d41ca238-7aca-4939-9f34-063ea6b03901.png" width="600" /></p>  
  
์ด์ ๊ฐ์ด $l$๊ฐ์ feature๋ฅผ ๊ฐ์ง ๋ฐ์ดํฐ์ ๋ชจ๋  feature์ ๋ํด์ Basic Minkowski Distance๋ ์๋์ ๊ฐ์ด ์ ์๋๋ค.<br>  
  
<center>$d(i,j)\;=^p\sqrt{|x_{i1}-x_{j1}|^p+|x_{i2}-x_{j2}|^p+...+|x_{il}-x_{jl}|^p}$</center><br>  

๊ทธ๋ฆฌ๊ณ  ์ด๋์ $p$๊ฐ์ ๋ํด์ Minkowski Distance๋ฅผ <b><a>$L-p\;norm$</a></b> ์ด๋ผ ํ๋ค.  
  
Minkowski Distance ๋ ๋ช๊ฐ์ง ์ฑ์ง์ ๊ฐ์ง๊ณ  ์๋๋ฐ,  
- $d(i,j)>0\;\;(when\;\;i\neq{j})$<br>  
- $d(i,i)=0\;\;\,(positivity)$<br>  
- $d(i,j)=d(j,i)\;\;(symmetry)$<br>  
- $d(i,j)\leqq{d(i,k)}+d(k,j)\;\;(Triangle\;Inequality)$<br>  
  
๋งจ ๋ง์ง๋ง ์ฑ์ง์ด ์ดํด๊ฐ ์ ๊ฐ ์ ์๋๋ฐ, ์ด๋ $i,j,k$ ์ธ ์ ์ด ์ผ๊ฐํ์ ์ด๋ฃฐ ๋๋ผ๊ณ  ์๊ฐํ๋ฉด ๋๋ค. ํ ๋ณ์ ๊ธธ์ด๊ฐ ๋๋ณ์ ๊ธธ์ด์ ํฉ๋ณด๋ค ์์์ผ ํ๋ค๋ ์ผ๊ฐํ์ ์์ฑ์กฐ๊ฑด์ ์ํ ์ฑ์ง์ด๋ค.  

๐งฉ ์์์ ์ธ๊ธํ๋ฏ์ด Minkowski distance๋ $p$๊ฐ์ ์ํด ์์๊ณผ ์ด๋ฆ์ด ๋ฌ๋ผ์ง๋ค. ์ด์ ๋ ๊ทธ ๊ฒฝ์ฐ์ ๋ํด ์์๋ณด๋๋ก ํ์.  

* * *  
## 2. L-p Norm  

- p = 1 ์ธ ๊ฒฝ์ฐ  
    - L<sub>1</sub> Norm, <b><a>Manhattan Distance</a></b>  
    - ๋จ์ ๊ฑฐ๋ฆฌ์ ํฌ๊ธฐ์ ํฉ.  

<center>$d(i,j)\;=|x_{i1}-x_{j1}|+|x_{i2}-x_{j2}|+...+|x_{il}-x_{jl}|$</center>  

- p = 2 ์ธ ๊ฒฝ์ฐ  
    - L<sub>2</sub> Norm, <b><a>Euclidean Distance</a></b><br>  
    - ํํ ์ํ์์ ์ ํ  ์ ์๋ ๋ ์  ์ฌ์ด์ ๊ฑฐ๋ฆฌ ๊ณต์.  
  
<center>$d(i,j)\;=\sqrt{|x_{i1}-x_{j1}|^2+|x_{i2}-x_{j2}|^2+...+|x_{il}-x_{jl}|^2}$</center><br>  

- p  $\rightarrow$ โ ์ธ ๊ฒฝ์ฐ  
    - L<sub>max</sub> Norm, L<sub>โ</sub> Norm, <b><a>Supremum Distance</a></b>  
    - ๊ฑฐ๋ฆฌ์ ํฌ๊ธฐ๋ค ์ค ์ต๋๊ฐ์ ์ ํ.  

<center>$d(i,j)\;=max(|x_{i1}-x_{j1}|,\,|x_{i2}-x_{j2}|,\,...,\,|x_{il}-x_{jl}|)$</center><br>  

๐งฉ ๋น์ฐํ, ์ด Mimkowski Distance์ ๊ฒฐ๊ณผ ์ญ์ Distance Matrix์ ํํ๋ก ๋ง๋ค์ด ์ค ์ ์๋ค. ๊ด๋ จ ๋งํฌ๋ฅผ ์ฒจ๋ถํด ๋์์ผ๋ ํ์ํ ์ฌ๋์ ์ฐธ๊ณ ํด๋ ์ข์ ๊ฒ ๊ฐ๋ค๐.  

[๐ Distance Matrix ๊ด๋ จ ํฌ์คํ](https://nyamin9.github.io/data_mining/Data-Mining-Distance-1/).  

* * *  

๐งฉ ์ด๋ฒ ํฌ์คํ์์๋ Numerical Attribute์ distance measure๋ฅผ ๋ค๋ค๋ณด์๋ค. ์์์ ๋ฃจํธ๋ ๋ค์ด๊ฐ ์์ด์ ์ฝ๊ฐ ๊ท์ฐฎ์๋ณด์ผ ์ ์์ง๋ง, ๊ทธ ๋ฐฉ์์ ์๊ฐ๋ณด๋ค ๊ฐ๋จํ๊ธฐ ๋๋ฌธ์ ์ง์  ๊ตฌํํด ๋ณด๋ ๊ฒ๋ ์ด๋ ต์ง ์์ ๊ฒ์ด๋ผ ์๊ฐํ๋ค. ๋ค์ ํฌ์คํ์์๋ Document frequency๋ฅผ ์ํ distance measure๋ฅผ ๋ฐฐ์๋ณด์๐โโ๏ธ๐โโ๏ธ.  

* * *  
<div style="text-align: left">๐ก์ ํฌ์คํ์ ํ๊ตญ์ธ๊ตญ์ด๋ํ๊ต ๋ฐ์ด์ค๋ฉ๋์ปฌ๊ณตํ๋ถ ๊ณ ์คํฌ ๊ต์๋์ [์๋ช์ ๋ณดํ์ ์ํ ๋ฐ์ดํฐ๋ง์ด๋] ๊ฐ์ ๋ด์ฉ์ ๋ฐํ์ผ๋ก ํจ์ ๋ฐํ๋๋ค.</div>

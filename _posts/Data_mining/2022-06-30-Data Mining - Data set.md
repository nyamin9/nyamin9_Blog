---
title : "๐งฉ Data Mining (2) - Data set"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Distance]

toc : true
toc_sticky : true

date: 2022-06-30
last_modified_at: 2022-06-30
---  
* * *  

๐งฉ ์ฐ๋ฆฌ๊ฐ ๋ค๋ฃฐ ๋ฐ์ดํฐ์๋ ์ ๋ง ๋ง์ ์ข๋ฅ๊ฐ ์๋ค. ์ซ์๋ก ํํ๋ ํ์๋ ์์ ๊ฒ์ด๊ณ , ํ์กํ์ฒ๋ผ ๋ฒ์ฃผํ์ผ๋ก ํํ๋ ๋ฐ์ดํฐ๋ ์์ ๊ฒ์ด๋ค. ๋ณธ๊ฒฉ์ ์ผ๋ก Distance measure์ ๋ํด ์์๋ณด๊ธฐ ์ ์, Data์ ๊ตฌ์กฐ๋ถํฐ ์์๋ณด๋๋ก ํ์.  

* * *  
  
## 1. Data ๊ตฌ์กฐ  
  
- Data Set์ <a>objects</a> (= observation)์ ์งํฉ : ํ (row)  
    - ex) customers / patients / students...  

- ๊ฐ data object ๋ <a>attribute</a> (= features)๋ก ํํ๋จ : ์ด (column)  
    - object๊ฐ ๊ฐ์ง๊ณ  ์๋ ์์ฑ  
    - ex) age / grade / department...  

``` 
    <Data Set>
                            features
                            1   2   3   4   ...
            objects  1
                     2
                     3
                     4
                     ...
```  
* * *  
## 2. Attributes Type  
 
- <b>Categorical Data</b>  

    - Nominal  
        - categories / states / ์ด๋ฆ / <a>์์ ์์</a>  
        - ex) Hair color / Blood type  
          
    - Binary  
        - <a>0 / 1</a> ์ ๋๊ฐ์ง state๋ก๋ง ํํ๋๋ data. nominal type.  
        - <a>Symmetric binary</a> : 0 / 1 ์ด ๋ฐ์ํ  ํ๋ฅ ์ด ๋น์ทํ์ฌ ์๋ก ๋์นญ์ ์ธ ๋ฐ์ดํฐ. ex) gender  
        - <a>Asymetric binary</a> : 0 / 1 ์ด ๋ฐ์ํ  ํ๋ฅ ์ ์ฐจ์ด๊ฐ ํฐ ๊ฒฝ์ฐ. ๋น๋์นญ์ ์ธ ๋ฐ์ดํฐ. ex) ์ง๋ณ์ ์์ฑ / ์์ฑ  

    - Ordinal  
        - ranking / <a>์์ ์์</a>  
        - ex) size / grade / ์ค๋ฌธ์กฐ์ฌ ๊ฒฐ๊ณผ  


- <b>Numerical Data</b>  
  
    - Discrete  
        - <a>์ ์</a> / ์ด์ฐํ / ์นด์ดํธ ๊ฐ๋ฅ. ex) age  
        - binary type์ ํน๋ณํ ๊ฒฝ์ฐ์ discrete data type ์ด๋ค.  
      
    - Continuous  
        - <a>์ค์</a> / ์ฐ์ํ. ex) ๊ธฐ์จ / ์ฒด์จ / ํค / ๋ชธ๋ฌด๊ฒ  
          
* * *  
๐งฉ ์ด๋ฒ ํฌ์คํ์์๋ data set์ ๊ตฌ์กฐ์ ์๋ฃํ์ ๋ฐ๋ฅธ ๋ถ๋ฅ์ ๋ํด ๊ฐ๋ตํ๊ฒ ์์๋ณด์๋ค. ์์ผ๋ก ์ฌ์ฉํ  ๋ง์ measure๋ค์ด ์๋ฃํ์ ๋ฐ๋ผ ๋ค๋ฅด๊ฒ ์ ์ฉ๋๋ ๊ฒฝ์ฐ๊ฐ ์๊ธฐ ๋๋ฌธ์, ๊ฐ๋จํ์ง๋ง ํ์คํ๊ฒ ์๊ณ  ๋์ด๊ฐ๋ ๊ฒ์ด ์ค์ํ  ๊ฑฐ๋ผ๊ณ  ์๊ฐํ๋ค๐.  
  
๐งฉ ๋ค์ ํฌ์คํ์์๋ ๋ฐ์ดํฐ ์์์ object์ ์์น๋ฅผ ์์๋ผ ์ ์๋ Quatile plot๊ณผ scatter plot์ ๋ํด ์์๋ณด์.  
  
* * *  
<div style="text-align: left">๐ก์ ํฌ์คํ์ ํ๊ตญ์ธ๊ตญ์ด๋ํ๊ต ๋ฐ์ด์ค๋ฉ๋์ปฌ๊ณตํ๋ถ ๊ณ ์คํฌ ๊ต์๋์ [์๋ช์ ๋ณดํ์ ์ํ ๋ฐ์ดํฐ๋ง์ด๋] ๊ฐ์ ๋ด์ฉ์ ๋ฐํ์ผ๋ก ํจ์ ๋ฐํ๋๋ค.</div>

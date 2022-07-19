---
title : "🧩 Data Mining (15) - Preprocessing_8 : Data Reduction - Dimensionality"

categories:
    - Data_mining
tags:
    - [Pandas, Data, Data Mining, Preprocessing, Reduction, Dimensionality]

toc : true
toc_sticky : true 
use_math : true  

date: 2022-07-19
last_modified_at: 2022-07-19 
---  
  
* * *  

🧩 저번 포스팅까지 해서 데이터의 object를 줄이는 Numerosity reduction를 다루었다. [파라미터를 사용하거나](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-5/) [사용하지 않는](https://nyamin9.github.io/data_mining/Data-Mining-Preprocessing-7/) 방법이 있다는 것만 알면 그 개념에 대한 정리는 끝낼 수 있을 것 같다. 이번 포스팅부터는 데이터의 attribute를 줄이는 <a><b>Dimensionality Reduction</b></a>에 대해 알아보도록 하자.  

* * *  
## 1. Dimensionality Reduction 개념  

🧩 이때까지 다뤄온 내용에서도 그랬지만, 데이터가 지나치게 복잡하면 정말 필요한 정보를 뽑아내기가 어렵다. 이러한 현상을 <a>Curse of Dimensionality</a>, 즉 dimension의 저주라고 한다. dimension이 증가하면 오히려 데이터에 결측값이나 관련없는 값 등의 빈 공간이 많아져서 원하는 정보를 얻기가 어렵다는 의미이다. 또한 <b>diemnsion이 너무 많으면 정말 중요한 attribute의 중요도가 약화되면서 오히려 중요성이 가려질 수 있다</b>. 이러한 이유로 dimension을 줄여줘야 하는데, 이를 줄이는 과정을 Dimensionality Reduction이라 한다.<br>  


⭐ <b>Dimensionality Reduction</b><br>  
- random variables의 수를 줄여서 정말 중요한 variables를 얻는 것<br>  

⭐ <b>Dimensionality Reduction의 장점</b><br>  
- curse of dimensionality reduction을 줄일 수 있음  
- 상관없는 attribute / noise 제거  
- 데이터 마이닝에 드는 시간과 노력을 줄일 수 있음  
- 보다 수월한 시각화 가능<br>  

* * *  
## 2. Dimensionality Reduction Methology  

🧩 위에서 Dimensionality Reduction의 개념과 장점을 알아보았다. 이름이 길어서 조금 어려워 보일 수 있지만 하는 이유는 지극히 단순하다. 하지만 그 간단한 이유를 위해 수행해야 하는 과정이 마냥 단순하다고 할 수 는 없을 것 같다. 대부분의 데이터를 흝어봐야 하는 것은 물론이고, 이 중에서도 어느 정도 관련이 있는 부분들에만 집중해야 하기 때문이다. 이제는 이 복잡한 방법들에 뭐가 있을지 알아보도록 하자🙃🙃.<br>  

- <b>1. Feature Selection</b><br>  
    - attribute로부터 데이터를 잘 설명해주는 subset을 찾는 것  
    - 필요한 attribute만 골라내서 새로운 attribute의 집합을 만드는 것  
    - ex) <a>Feature Subset Selection</a> / Feature Creation<br>  

- <b>2. Feature Extraction</b><br>  
    - high-dimensional space data를 fewer dimension으로 변환  
    - 여러 attribute를 가지고 새로운 attribute를 생성함  
    - ex) <a>Principal Componenet Analysis (PCA)</a><br>  


* * *  

🧩 이렇게 해서 <b>Dimensionality Reduction</b>의 개념을 간단하게 핵심만 살펴보았다. 보다 원할한 데이터 마이닝을 위한 데이터의 전처리 과정이라고 이해하면 될 것 같다. 다음 포스팅부터는 Dimensionality Reduction의 방법들을 알아볼텐데, 첫번째로 <a>Feature Selection</a>에 대해 알아보도록 하자🏃‍♂️🏃‍♂️!!  

* * *  
<div style="text-align: left">💡위 포스팅은 한국외국어대학교 바이오메디컬공학부 고윤희 교수님의 [생명정보학을 위한 데이터마이닝] 강의 내용을 바탕으로 함을 밝힙니다.</div>
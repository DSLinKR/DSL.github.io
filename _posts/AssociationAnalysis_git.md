# Clustering


```python
from plotnine import *
%matplotlib inline
import matplotlib.cm as cm
import matplotlib
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
font_location = '/usr/share/fonts/truetype/nanum/NanumGothic.ttf'
font_name = matplotlib.font_manager.FontProperties(fname=font_location).get_name()
matplotlib.rc('font', family=font_name)
```

## 개념

unsuperbised learning

Data type에 따라 적절한 모델을 사용해야한다

EDA로 사용할 수 있다

### K-means

Numrical

 ### K-modes

categorical

### K-prototype

mixed type

## packages

use sklearn cluster package or kmodes


```python
from sklearn.cluster import KMeans
from kmodes.kmodes import KModes
from kmodes.kprototypes import KPrototypes
```


```python
KME = KMeans(n_clusters=4)
KMO = KModes(n_clusters=4, init='Huang', n_init=5, verbose=1)
KP = KPrototypes(n_clusters=5, verbose=1, gamma=None)
```

## Data

노래 하나 하나는 카테고리이므로, 노래만으로 클러스터를 하려면 KMO를, like count까지 쓰려면 KP를

KMO로 like_cnt에 따른 클러스터링이 될까?


```python
ap
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Love Blossom (러브블러썸)</th>
      <th>No Make Up</th>
      <th>체념</th>
      <th>고백(Go Back) (Feat.정인)</th>
      <th>Love Lane</th>
      <th>겨울 고백</th>
      <th>묘해, 너와</th>
      <th>Going Home</th>
      <th>남이 될 수 있을까</th>
      <th>무릎</th>
      <th>...</th>
      <th>ifuleave (Feat. Mary J. Blige) (Album Ver.)</th>
      <th>우린 알아</th>
      <th>빨간 맛 (Red Flavor)</th>
      <th>음오아예 (Um Oh Ah Yeh)</th>
      <th>Faded</th>
      <th>Don`t Know Why</th>
      <th>잠 못 드는 밤에</th>
      <th>FOOLS</th>
      <th>슬픔활용법</th>
      <th>꿈처럼</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9190</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9191</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9192</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9193</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9194</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>...</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>9195 rows × 1003 columns</p>
</div>




```python
cluster = KMO.fit_predict(ap)
```

    Init: initializing centroids
    Init: initializing clusters
    Starting iterations...
    Run 1, iteration: 1/100, moves: 4314, cost: 300744.0
    Run 1, iteration: 2/100, moves: 213, cost: 299006.0
    Run 1, iteration: 3/100, moves: 29, cost: 299006.0
    Init: initializing centroids
    Init: initializing clusters
    Starting iterations...
    Run 2, iteration: 1/100, moves: 6051, cost: 306640.0
    Run 2, iteration: 2/100, moves: 360, cost: 306324.0
    Run 2, iteration: 3/100, moves: 119, cost: 306324.0
    Init: initializing centroids
    Init: initializing clusters
    Starting iterations...
    Run 3, iteration: 1/100, moves: 2954, cost: 300308.0
    Run 3, iteration: 2/100, moves: 178, cost: 300024.0
    Run 3, iteration: 3/100, moves: 24, cost: 300024.0
    Init: initializing centroids
    Init: initializing clusters
    Starting iterations...
    Run 4, iteration: 1/100, moves: 6148, cost: 306221.0
    Run 4, iteration: 2/100, moves: 54, cost: 306079.0
    Run 4, iteration: 3/100, moves: 19, cost: 306054.0
    Run 4, iteration: 4/100, moves: 13, cost: 306032.0
    Run 4, iteration: 5/100, moves: 1, cost: 306032.0
    Init: initializing centroids
    Init: initializing clusters
    Starting iterations...
    Run 5, iteration: 1/100, moves: 4244, cost: 306904.0
    Run 5, iteration: 2/100, moves: 215, cost: 304815.0
    Run 5, iteration: 3/100, moves: 78, cost: 304597.0
    Run 5, iteration: 4/100, moves: 16, cost: 304592.0
    Run 5, iteration: 5/100, moves: 0, cost: 304592.0
    Best run was number 1



```python
cluster
```




    array([2, 1, 1, ..., 1, 1, 1], dtype=uint16)




```python
from collections import Counter
Counter(cluster)
```




    Counter({2: 204, 1: 7140, 0: 1139, 3: 712})




```python
col = pd.Series(cluster).map({0:'b',1:'yellow',2:'k', 3:'r'})
```


```python
plt.scatter(ply[col!='yellow'].songs.apply(len), ply[col!='yellow']['like_cnt'],c=col[col!='yellow'])
```




    <matplotlib.collections.PathCollection at 0x7f764e3c7240>




![png](AssociationAnalysis_git_files/AssociationAnalysis_git_25_1.png)



```python
plt.scatter(ply.songs.apply(len), ply['like_cnt'],c=col)
```




    <matplotlib.collections.PathCollection at 0x7f764e375a58>




![png](AssociationAnalysis_git_files/AssociationAnalysis_git_26_1.png)


like count가 낮은 친구들이 클러스터가 되긴 됐다. 이 친구들이 가지고 있는 노래들의 특징: 인기가 없다?  
count data는 포아송분포를 따른다, 대략 포아송분포임을 눈으로 확인할 수 있었다. 즉, black과 yellow는 의미없음

# Association Rules

## 개념

### Confidence

X를 샀을 때, Y를 샀을 확률

\begin{align}
\frac{P(X \cap Y)}{P(X)}
\end{align}

### Support

전체 상품(A) 중 상품 X와 상품 Y를 동시에 살 확률

\begin{align}
\frac{P(X \cap Y)}{P(A)}
\end{align}

Confidence가 100이라 하더라도 support가 낮으면 추천해줘야할까?

좋은 규칙, 구성비가 높고 빈도가 많은 규칙, 을 찾거나 불필요한 연산을 줄위기 위한 기준으로 사용된다

별로 팔리지 않는 상품을 걸러내기 위함

### Lift

Y를 구매한 비율과 X를 구매한 사람 중 Y를 구매한 비율을 비교함

\begin{align}
\frac{\frac{P(X \cap Y)}{P(X)}}{\frac{P(Y)}{P(A)}}
\end{align}

많이 팔리는 인기상품을 골라내기 위해 사용됨. 1보다 작으면 좋지 못하다

### Antecednet and Consequents

조건절과 결과절

## Packages


```python
import itertools
import json
import math
```


```python
import numpy as np
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori, association_rules
import networkx as nx
```

## Data

### Load


```python
meta.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>song_gn_dtl_gnr_basket</th>
      <th>issue_date</th>
      <th>album_name</th>
      <th>album_id</th>
      <th>artist_id_basket</th>
      <th>song_name</th>
      <th>song_gn_gnr_basket</th>
      <th>artist_name_basket</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>['GN0401', 'GN0403']</td>
      <td>20150205</td>
      <td>브라운 아이드 소울 싱글 프로젝트 1st. 같은 시간 속의 너 By 나얼</td>
      <td>2302870</td>
      <td>[3959]</td>
      <td>같은 시간 속의 너</td>
      <td>['GN0400']</td>
      <td>['나얼']</td>
      <td>169984</td>
    </tr>
    <tr>
      <th>1</th>
      <td>['GN0104', 'GN0101']</td>
      <td>20070419</td>
      <td>나무로 만든 노래</td>
      <td>350016</td>
      <td>[1088]</td>
      <td>다행이다</td>
      <td>['GN0100']</td>
      <td>['이적']</td>
      <td>104450</td>
    </tr>
    <tr>
      <th>2</th>
      <td>['GN0105', 'GN0101', 'GN2505', 'GN2503', 'GN15...</td>
      <td>20161231</td>
      <td>도깨비 OST Part.7</td>
      <td>10027253</td>
      <td>[490981]</td>
      <td>I Miss You</td>
      <td>['GN2500', 'GN1500', 'GN0100']</td>
      <td>['소유 (SOYOU)']</td>
      <td>608260</td>
    </tr>
    <tr>
      <th>3</th>
      <td>['GN2704', 'GN1102', 'GN1101']</td>
      <td>20150615</td>
      <td>Roses (Feat. ROZES)</td>
      <td>2324717</td>
      <td>[713297]</td>
      <td>Roses (Feat. ROZES)</td>
      <td>['GN2700', 'GN1100']</td>
      <td>['The Chainsmokers']</td>
      <td>501764</td>
    </tr>
    <tr>
      <th>4</th>
      <td>['GN0105', 'GN0101']</td>
      <td>20161129</td>
      <td>목소리</td>
      <td>10018979</td>
      <td>[792091]</td>
      <td>이 바보야</td>
      <td>['GN0100']</td>
      <td>['정승환']</td>
      <td>118788</td>
    </tr>
  </tbody>
</table>
</div>




```python
ply.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tags</th>
      <th>id</th>
      <th>plylst_title</th>
      <th>songs</th>
      <th>like_cnt</th>
      <th>updt_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>['kpop', '댄스', '걸그룹댄스', '스트레스해소']</td>
      <td>31804</td>
      <td>걸그룹 땐쓰쏭</td>
      <td>[113664, 375431, 455945, 342798, 380564, 51842...</td>
      <td>74</td>
      <td>2020-04-13 23:36:55.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>['80년대', '감성', '90년대발라드', '올드송', '추억', '휴식', '...</td>
      <td>131098</td>
      <td>8~90년대 우리나라 라디오에서 흘러나오던 명곡들.</td>
      <td>[481669, 635537, 346897, 61595, 243099, 370203...</td>
      <td>53</td>
      <td>2019-11-25 17:25:12.000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>['기분전환', '설렘', '사랑']</td>
      <td>124665</td>
      <td>여자가 좋아하는 남자노래방곡들~</td>
      <td>[104450, 663564, 625933, 486938, 243099, 23951...</td>
      <td>83</td>
      <td>2017-11-28 11:44:44.000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>['조용한', '밤', '새벽']</td>
      <td>8455</td>
      <td>혼자남겨진밤..</td>
      <td>[169984, 413314, 118788, 54408, 377355, 655756...</td>
      <td>0</td>
      <td>2017-07-25 19:45:23.000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>['포근함', '봄', '따스한', '벚꽃', '힐링', '사랑', '신나는']</td>
      <td>125944</td>
      <td>''흔들리는 벚꽃 속에서'' 들어야하는 봄 노래</td>
      <td>[132994, 204547, 283138, 243850, 257434, 58178...</td>
      <td>49</td>
      <td>2020-04-03 08:12:36.000</td>
    </tr>
  </tbody>
</table>
</div>




```python
ply['songs'] = ply.songs.apply(lambda x: json.loads(x))
```

### Song Mapping


```python
song_to_name={}
for i in range(len(meta)):
    song_to_name[meta.id[i]] = meta.song_name[i]
```

### PreProcessing

Association Rule을 적용하기 위해서 TransactionEncoder를 사용해 dataset을 변환해준다


```python
dataset=[]
for i in range(len(ply)):
    dataset.append(ply.songs[i])
```


```python
te = TransactionEncoder()
te_ary = te.fit(dataset).transform(dataset)
```

## Apply model


```python
ap = pd.DataFrame(te_ary, columns=te.columns_)
ap.columns = [song_to_name[x] for x in ap.columns]
ap.sum().to_frame('Frequency').sort_values('Frequency',ascending=False)[:25].plot(kind='bar',
                                                                                  figsize=(12,8),
                                                                                  title="Frequent Items")
plt.show()
```


![png](AssociationAnalysis_git_files/AssociationAnalysis_git_60_0.png)


dataset에서 가장 많이 등장한 노래를 보여준다. 우리가 자주 보지 못하던 노래들이다. 아마 특정 DJ가 주로 사용하는 노래이지만 인지도가 없는 노래일 가능성이 높다


```python
frequent_itemsets = apriori(ap, min_support=0.14, use_colnames=True, verbose=1)
frequent_itemsets.head(10)
```

    Processing 30 combinations | Sampling itemset size 5





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>support</th>
      <th>itemsets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.149864</td>
      <td>(벙어리)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.147580</td>
      <td>(착각)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.144318</td>
      <td>(Sad Movie (Vocal by Levi))</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.150843</td>
      <td>(지워줄게 (Vocal by 스티브언니))</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.161066</td>
      <td>(비가 내렸어 (Vocal by 스티브언니))</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.141925</td>
      <td>(선물)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.160848</td>
      <td>(고마운 사람 (Vocal by 이소진))</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.148124</td>
      <td>(사랑을 놓치고)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.149429</td>
      <td>(분홍빛 가득한 날에 (Vocal by 호수))</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.146601</td>
      <td>(끝내지 못한 이야기 (Feat. 호수))</td>
    </tr>
  </tbody>
</table>
</div>



apriori 명령어를 써도 frequent_itemset을 뽑아낼 수 있고, minimum support를 지정해줄 수 있다


```python
rules = association_rules(frequent_itemsets, metric="lift", min_threshold=0.5).head(50)
```


```python
rules.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>antecedents</th>
      <th>consequents</th>
      <th>antecedent support</th>
      <th>consequent support</th>
      <th>support</th>
      <th>confidence</th>
      <th>lift</th>
      <th>leverage</th>
      <th>conviction</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(착각)</td>
      <td>(벙어리)</td>
      <td>0.147580</td>
      <td>0.149864</td>
      <td>0.146710</td>
      <td>0.994105</td>
      <td>6.633376</td>
      <td>0.124593</td>
      <td>144.204309</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(벙어리)</td>
      <td>(착각)</td>
      <td>0.149864</td>
      <td>0.147580</td>
      <td>0.146710</td>
      <td>0.978955</td>
      <td>6.633376</td>
      <td>0.124593</td>
      <td>40.504637</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(벙어리)</td>
      <td>(비가 내렸어 (Vocal by 스티브언니))</td>
      <td>0.149864</td>
      <td>0.161066</td>
      <td>0.142686</td>
      <td>0.952104</td>
      <td>5.911277</td>
      <td>0.118548</td>
      <td>17.515929</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(비가 내렸어 (Vocal by 스티브언니))</td>
      <td>(벙어리)</td>
      <td>0.161066</td>
      <td>0.149864</td>
      <td>0.142686</td>
      <td>0.885888</td>
      <td>5.911277</td>
      <td>0.118548</td>
      <td>7.450008</td>
    </tr>
    <tr>
      <th>4</th>
      <td>(벙어리)</td>
      <td>(고마운 사람 (Vocal by 이소진))</td>
      <td>0.149864</td>
      <td>0.160848</td>
      <td>0.142469</td>
      <td>0.950653</td>
      <td>5.910247</td>
      <td>0.118363</td>
      <td>17.005163</td>
    </tr>
    <tr>
      <th>5</th>
      <td>(고마운 사람 (Vocal by 이소진))</td>
      <td>(벙어리)</td>
      <td>0.160848</td>
      <td>0.149864</td>
      <td>0.142469</td>
      <td>0.885734</td>
      <td>5.910247</td>
      <td>0.118363</td>
      <td>7.439947</td>
    </tr>
    <tr>
      <th>6</th>
      <td>(벙어리)</td>
      <td>(사랑을 놓치고)</td>
      <td>0.149864</td>
      <td>0.148124</td>
      <td>0.147254</td>
      <td>0.982583</td>
      <td>6.633520</td>
      <td>0.125055</td>
      <td>48.911881</td>
    </tr>
    <tr>
      <th>7</th>
      <td>(사랑을 놓치고)</td>
      <td>(벙어리)</td>
      <td>0.148124</td>
      <td>0.149864</td>
      <td>0.147254</td>
      <td>0.994126</td>
      <td>6.633520</td>
      <td>0.125055</td>
      <td>144.735644</td>
    </tr>
    <tr>
      <th>8</th>
      <td>(착각)</td>
      <td>(비가 내렸어 (Vocal by 스티브언니))</td>
      <td>0.147580</td>
      <td>0.161066</td>
      <td>0.143121</td>
      <td>0.969786</td>
      <td>6.021057</td>
      <td>0.119351</td>
      <td>27.766676</td>
    </tr>
    <tr>
      <th>9</th>
      <td>(비가 내렸어 (Vocal by 스티브언니))</td>
      <td>(착각)</td>
      <td>0.161066</td>
      <td>0.147580</td>
      <td>0.143121</td>
      <td>0.888589</td>
      <td>6.021057</td>
      <td>0.119351</td>
      <td>7.651113</td>
    </tr>
  </tbody>
</table>
</div>




```python
def draw_graph(rules, rules_to_show):
    G1 = nx.DiGraph()
   
    color_map=[]
    N = 50
    colors = np.random.rand(N)    
    strs=['R0', 'R1', 'R2', 'R3', 'R4', 'R5', 'R6', 'R7', 'R8', 'R9', 'R10',
         'R11', 'R12', 'R13', 'R14', 'R15', 'R16', 'R17', 'R18', 'R19', 'R20']   
   
   
    for i in range (rules_to_show):
        G1.add_nodes_from(["R"+str(i)])
        
        for a in rules.iloc[i]['antecedents']:
                
            G1.add_nodes_from([a])
        
            G1.add_edge(a, "R"+str(i), color=colors[i] , weight = 2)
       
        for c in rules.iloc[i]['consequents']:
             
            G1.add_nodes_from([c])
            
            G1.add_edge("R"+str(i), c, color=colors[i],  weight=2)
 
    for node in G1:
        found_a_string = False
        for item in strs: 
            if node==item:
                found_a_string = True
        if found_a_string:
            color_map.append('yellow')
        else:
            color_map.append('green')       
 
 
   
    edges = G1.edges()
    colors = [G1[u][v]['color'] for u,v in edges]
    weights = [G1[u][v]['weight'] for u,v in edges]
   
    pos = nx.spring_layout(G1, k=16, scale=1)
    nx.draw(G1, pos, edges=edges, node_color = color_map, edge_color=colors ,width=weights, font_size=16, with_labels=False)            
     
    for p in pos:  # raise text positions
             pos[p][1] += 0.07
    nx.draw_networkx_labels(G1, pos, font_family=font_name)
    plt.show()
```


```python
draw_graph(rules, 10)
```


![png](AssociationAnalysis_git_files/AssociationAnalysis_git_67_0.png)



```python
def draw_graph(rules, rules_to_show):
    plt.figure(figsize=(20,20))
    G1 = nx.DiGraph() #데이터 넣기
   
    color_map=[]  
    strs=['R'+str(x) for x in range(0,rules_to_show)]   
   
   
    for i in range (rules_to_show):      
        G1.add_nodes_from(["R"+str(i)], weight = 100)
    
     
        for a in rules.iloc[i]['antecedents']:
                
            G1.add_nodes_from([a])
        
            G1.add_edge(a, "R"+str(i), color="black" , weight = 2)
       
        for c in rules.iloc[i]['consequents']:
             
            G1.add_nodes_from([c])
            
            G1.add_edge("R"+str(i), c, color="black",  weight=2) #화살표
 
    edges = G1.edges()
    colors = [G1[u][v]['color'] for u,v in edges]
    weights = [G1[u][v]['weight'] for u,v in edges]

    node_size = []
    for i in range(rules_to_show):
        node_size.append(rules.iloc[i]['support'])
    maxconf = max(node_size)
    multifier = 500/maxconf
    for i in range(rules_to_show):
        node_size[i] = node_size[i]*multifier
    size = []
    counter = 0
    for node in G1.nodes():
        if node in strs:
            size.append(node_size[counter])
            counter += 1
        else:
            size.append(0)



    cmap = cm.get_cmap('OrRd')
    node_color = []
    for i in range(rules_to_show):
        node_color.append(rules.iloc[i]['lift'])
    maxconf = max(node_color)
    multifier = 1/maxconf
    for i in range(rules_to_show):
        node_color[i] = cmap(node_color[i]*multifier)
    col = []
    counter = 0
    for node in G1.nodes():
        if node in strs:
            col.append(node_color[counter])
            counter += 1
        else:
            col.append(cmap(0))


    pos = nx.spring_layout(G1, dim=2, k=1.5/math.sqrt(rules_to_show), pos=None, fixed=None, iterations=50, weight='weight', scale=1.0)
    nx.draw(G1, pos, edges=edges, node_color = col, edge_color=colors, width=weights, font_size=26, with_labels=False,node_size=size)            



    labels = {}    
    for node in G1.nodes():
        if node not in strs:
            labels[node] = node
    nx.draw_networkx_labels(G1,pos,labels,font_size=13,font_color='r',font_family=font_name)
    plt.show()
```


```python
draw_graph(rules, 20)
```


![png](AssociationAnalysis_git_files/AssociationAnalysis_git_69_0.png)


like_cnt가 낮은 플레이리스트가 함께 있어 의미있는 정보를 뽑아내지 못한것 같아,like_cnt를 기반으로 다시 연관성 분석을 해보았다.

## Try another model


```python
(
    ggplot(ply)
    + geom_boxplot(aes(x=1, y='like_cnt'))
    + ggtitle("like_cnt")
    +ylim(0,200)

)
```

    /home/lds/anaconda3/envs/DL/lib/python3.7/site-packages/plotnine/layer.py:369: PlotnineWarning: stat_boxplot : Removed 834 rows containing non-finite values.



![png](AssociationAnalysis_git_files/AssociationAnalysis_git_72_1.png)





    <ggplot: (8759139758982)>



like_cnt가 40보다 큰 플레이리스트를 모아서 따로 해보자


```python
ply2 = ply[ply.like_cnt>40]
ply2 = ply2.reset_index(drop=True)
```


```python
ply2.shape
```




    (1828, 6)



총 1828개의 플레이리스트로 다시 연관성 분석을 진행해본다


```python
dataset2=[]
for i in range(len(ply2)):
    dataset2.append(ply2.songs[i])
te2 = TransactionEncoder()
te_ary2 = te2.fit(dataset2).transform(dataset2)
```


```python
ap2 = pd.DataFrame(te_ary2, columns=te2.columns_)
ap2.columns = [song_to_name[x] for x in ap2.columns]
```


```python
frequent_itemsets = apriori(ap2, min_support=0.05, use_colnames=True, verbose=1)
frequent_itemsets
```

    Processing 243 combinations | Sampling itemset size 3 2





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>support</th>
      <th>itemsets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.061269</td>
      <td>(Love Blossom (러브블러썸))</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.086980</td>
      <td>(체념)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.071116</td>
      <td>(묘해, 너와)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.060722</td>
      <td>(심장이 없어)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.061269</td>
      <td>(Lost Stars)</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>257</th>
      <td>0.053611</td>
      <td>(심쿵해 (Heart Attack), 오늘부터 우리는 (Me Gustas Tu))</td>
    </tr>
    <tr>
      <th>258</th>
      <td>0.053611</td>
      <td>(오늘부터 우리는 (Me Gustas Tu), SHAKE IT)</td>
    </tr>
    <tr>
      <th>259</th>
      <td>0.051969</td>
      <td>(OOH-AHH하게, CHEER UP)</td>
    </tr>
    <tr>
      <th>260</th>
      <td>0.050328</td>
      <td>(심쿵해 (Heart Attack), CHEER UP)</td>
    </tr>
    <tr>
      <th>261</th>
      <td>0.060175</td>
      <td>(심쿵해 (Heart Attack), SHAKE IT)</td>
    </tr>
  </tbody>
</table>
<p>262 rows × 2 columns</p>
</div>




```python
rules2 = association_rules(frequent_itemsets, metric="lift", min_threshold=0.1).head(50)
```


```python
rules2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>antecedents</th>
      <th>consequents</th>
      <th>antecedent support</th>
      <th>consequent support</th>
      <th>support</th>
      <th>confidence</th>
      <th>lift</th>
      <th>leverage</th>
      <th>conviction</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(Tell me)</td>
      <td>(Nobody)</td>
      <td>0.076586</td>
      <td>0.074398</td>
      <td>0.052516</td>
      <td>0.685714</td>
      <td>9.216807</td>
      <td>0.046819</td>
      <td>2.945096</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(Nobody)</td>
      <td>(Tell me)</td>
      <td>0.074398</td>
      <td>0.076586</td>
      <td>0.052516</td>
      <td>0.705882</td>
      <td>9.216807</td>
      <td>0.046819</td>
      <td>3.139606</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(So Hot)</td>
      <td>(Nobody)</td>
      <td>0.074398</td>
      <td>0.074398</td>
      <td>0.054158</td>
      <td>0.727941</td>
      <td>9.784386</td>
      <td>0.048622</td>
      <td>3.402212</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(Nobody)</td>
      <td>(So Hot)</td>
      <td>0.074398</td>
      <td>0.074398</td>
      <td>0.054158</td>
      <td>0.727941</td>
      <td>9.784386</td>
      <td>0.048622</td>
      <td>3.402212</td>
    </tr>
    <tr>
      <th>4</th>
      <td>(Tell me)</td>
      <td>(So Hot)</td>
      <td>0.076586</td>
      <td>0.074398</td>
      <td>0.051422</td>
      <td>0.671429</td>
      <td>9.024790</td>
      <td>0.045724</td>
      <td>2.817049</td>
    </tr>
    <tr>
      <th>5</th>
      <td>(So Hot)</td>
      <td>(Tell me)</td>
      <td>0.074398</td>
      <td>0.076586</td>
      <td>0.051422</td>
      <td>0.691176</td>
      <td>9.024790</td>
      <td>0.045724</td>
      <td>2.990101</td>
    </tr>
    <tr>
      <th>6</th>
      <td>(가시)</td>
      <td>(응급실)</td>
      <td>0.084792</td>
      <td>0.107768</td>
      <td>0.050875</td>
      <td>0.600000</td>
      <td>5.567513</td>
      <td>0.041737</td>
      <td>2.230580</td>
    </tr>
    <tr>
      <th>7</th>
      <td>(응급실)</td>
      <td>(가시)</td>
      <td>0.107768</td>
      <td>0.084792</td>
      <td>0.050875</td>
      <td>0.472081</td>
      <td>5.567513</td>
      <td>0.041737</td>
      <td>1.733615</td>
    </tr>
    <tr>
      <th>8</th>
      <td>(응급실)</td>
      <td>(눈의 꽃)</td>
      <td>0.107768</td>
      <td>0.105580</td>
      <td>0.053611</td>
      <td>0.497462</td>
      <td>4.711712</td>
      <td>0.042232</td>
      <td>1.779806</td>
    </tr>
    <tr>
      <th>9</th>
      <td>(눈의 꽃)</td>
      <td>(응급실)</td>
      <td>0.105580</td>
      <td>0.107768</td>
      <td>0.053611</td>
      <td>0.507772</td>
      <td>4.711712</td>
      <td>0.042232</td>
      <td>1.812640</td>
    </tr>
    <tr>
      <th>10</th>
      <td>(Touch My Body)</td>
      <td>(Darling)</td>
      <td>0.087527</td>
      <td>0.070569</td>
      <td>0.053611</td>
      <td>0.612500</td>
      <td>8.679457</td>
      <td>0.047434</td>
      <td>2.398532</td>
    </tr>
    <tr>
      <th>11</th>
      <td>(Darling)</td>
      <td>(Touch My Body)</td>
      <td>0.070569</td>
      <td>0.087527</td>
      <td>0.053611</td>
      <td>0.759690</td>
      <td>8.679457</td>
      <td>0.047434</td>
      <td>3.797064</td>
    </tr>
    <tr>
      <th>12</th>
      <td>(Touch My Body)</td>
      <td>(Loving U (러빙유))</td>
      <td>0.087527</td>
      <td>0.083151</td>
      <td>0.053611</td>
      <td>0.612500</td>
      <td>7.366118</td>
      <td>0.046333</td>
      <td>2.366062</td>
    </tr>
    <tr>
      <th>13</th>
      <td>(Loving U (러빙유))</td>
      <td>(Touch My Body)</td>
      <td>0.083151</td>
      <td>0.087527</td>
      <td>0.053611</td>
      <td>0.644737</td>
      <td>7.366118</td>
      <td>0.046333</td>
      <td>2.568442</td>
    </tr>
    <tr>
      <th>14</th>
      <td>(Touch My Body)</td>
      <td>(SHAKE IT)</td>
      <td>0.087527</td>
      <td>0.080963</td>
      <td>0.058534</td>
      <td>0.668750</td>
      <td>8.259966</td>
      <td>0.051447</td>
      <td>2.774452</td>
    </tr>
    <tr>
      <th>15</th>
      <td>(SHAKE IT)</td>
      <td>(Touch My Body)</td>
      <td>0.080963</td>
      <td>0.087527</td>
      <td>0.058534</td>
      <td>0.722973</td>
      <td>8.259966</td>
      <td>0.051447</td>
      <td>3.293804</td>
    </tr>
    <tr>
      <th>16</th>
      <td>(I Don`t Care)</td>
      <td>(Abracadabra)</td>
      <td>0.081510</td>
      <td>0.070569</td>
      <td>0.050328</td>
      <td>0.617450</td>
      <td>8.749597</td>
      <td>0.044576</td>
      <td>2.429565</td>
    </tr>
    <tr>
      <th>17</th>
      <td>(Abracadabra)</td>
      <td>(I Don`t Care)</td>
      <td>0.070569</td>
      <td>0.081510</td>
      <td>0.050328</td>
      <td>0.713178</td>
      <td>8.749597</td>
      <td>0.044576</td>
      <td>3.202304</td>
    </tr>
    <tr>
      <th>18</th>
      <td>(오늘부터 우리는 (Me Gustas Tu))</td>
      <td>(CHEER UP)</td>
      <td>0.084792</td>
      <td>0.087527</td>
      <td>0.052516</td>
      <td>0.619355</td>
      <td>7.076129</td>
      <td>0.045095</td>
      <td>2.397174</td>
    </tr>
    <tr>
      <th>19</th>
      <td>(CHEER UP)</td>
      <td>(오늘부터 우리는 (Me Gustas Tu))</td>
      <td>0.087527</td>
      <td>0.084792</td>
      <td>0.052516</td>
      <td>0.600000</td>
      <td>7.076129</td>
      <td>0.045095</td>
      <td>2.288020</td>
    </tr>
    <tr>
      <th>20</th>
      <td>(심쿵해 (Heart Attack))</td>
      <td>(오늘부터 우리는 (Me Gustas Tu))</td>
      <td>0.076586</td>
      <td>0.084792</td>
      <td>0.053611</td>
      <td>0.700000</td>
      <td>8.255484</td>
      <td>0.047117</td>
      <td>3.050693</td>
    </tr>
    <tr>
      <th>21</th>
      <td>(오늘부터 우리는 (Me Gustas Tu))</td>
      <td>(심쿵해 (Heart Attack))</td>
      <td>0.084792</td>
      <td>0.076586</td>
      <td>0.053611</td>
      <td>0.632258</td>
      <td>8.255484</td>
      <td>0.047117</td>
      <td>2.511037</td>
    </tr>
    <tr>
      <th>22</th>
      <td>(오늘부터 우리는 (Me Gustas Tu))</td>
      <td>(SHAKE IT)</td>
      <td>0.084792</td>
      <td>0.080963</td>
      <td>0.053611</td>
      <td>0.632258</td>
      <td>7.809241</td>
      <td>0.046745</td>
      <td>2.499136</td>
    </tr>
    <tr>
      <th>23</th>
      <td>(SHAKE IT)</td>
      <td>(오늘부터 우리는 (Me Gustas Tu))</td>
      <td>0.080963</td>
      <td>0.084792</td>
      <td>0.053611</td>
      <td>0.662162</td>
      <td>7.809241</td>
      <td>0.046745</td>
      <td>2.709015</td>
    </tr>
    <tr>
      <th>24</th>
      <td>(OOH-AHH하게)</td>
      <td>(CHEER UP)</td>
      <td>0.072210</td>
      <td>0.087527</td>
      <td>0.051969</td>
      <td>0.719697</td>
      <td>8.222538</td>
      <td>0.045649</td>
      <td>3.255308</td>
    </tr>
    <tr>
      <th>25</th>
      <td>(CHEER UP)</td>
      <td>(OOH-AHH하게)</td>
      <td>0.087527</td>
      <td>0.072210</td>
      <td>0.051969</td>
      <td>0.593750</td>
      <td>8.222538</td>
      <td>0.045649</td>
      <td>2.283791</td>
    </tr>
    <tr>
      <th>26</th>
      <td>(심쿵해 (Heart Attack))</td>
      <td>(CHEER UP)</td>
      <td>0.076586</td>
      <td>0.087527</td>
      <td>0.050328</td>
      <td>0.657143</td>
      <td>7.507857</td>
      <td>0.043625</td>
      <td>2.661379</td>
    </tr>
    <tr>
      <th>27</th>
      <td>(CHEER UP)</td>
      <td>(심쿵해 (Heart Attack))</td>
      <td>0.087527</td>
      <td>0.076586</td>
      <td>0.050328</td>
      <td>0.575000</td>
      <td>7.507857</td>
      <td>0.043625</td>
      <td>2.172738</td>
    </tr>
    <tr>
      <th>28</th>
      <td>(심쿵해 (Heart Attack))</td>
      <td>(SHAKE IT)</td>
      <td>0.076586</td>
      <td>0.080963</td>
      <td>0.060175</td>
      <td>0.785714</td>
      <td>9.704633</td>
      <td>0.053974</td>
      <td>4.288840</td>
    </tr>
    <tr>
      <th>29</th>
      <td>(SHAKE IT)</td>
      <td>(심쿵해 (Heart Attack))</td>
      <td>0.080963</td>
      <td>0.076586</td>
      <td>0.060175</td>
      <td>0.743243</td>
      <td>9.704633</td>
      <td>0.053974</td>
      <td>3.596453</td>
    </tr>
  </tbody>
</table>
</div>




```python
draw_graph(rules2, 20)
```


![png](AssociationAnalysis_git_files/AssociationAnalysis_git_82_0.png)


support가 매우 낮다. 하지만 인기가 많은 플레이리스트 중 2000년대, 2010년 초반, 2010년 중반 유행했던 여자아이돌 곡과 발라드곡의 연관성 그래프가 그려졌다. 특이한 점이 있다면 응급실을 매개로 2000년대 발라드와 2000년대 아이돌 곡이 묶였다.

---
title: "COVID 19 EDA with Plotnine"
date: 2020-07-09
classes: wide
toc: true
categories: Visualization DataAnalysis
---


# What is EDA?

탐색적 자료 분석, 시간을 들여 데이터에 대해 하나 하나 뜯어보는 것

데이터의 타입, 데이터의 결측치, 데이터 시각화 등이 여기에 들어간다

데이터 타입부터 살펴보자

## Data Type

### Categorical

#### Ordinary(순서자료)

범주형이지만(numerical이 아니지만) 순서가 존재하는 데이터. 스케일링의 문제가 있지만, continuous와 유사하게 사용해도 된다.

#### Nominal(명목형)

쉽게 말해서 범주형 자료이다. 독립변수로 사용될때는 One-hot encoding을 통해 표현해주면 된다. 종속 변수일때는 classify, 분류의 대상이 된다

### Numerical

(Continous) 혹은 (Discrete)

#### Interval

#### Ratio

## Missing Value

쉽게 최빈값, 평균값을 사용하기도 한다  
EM 알고리즘, 혹은 GAN을 사용할 수도 있다

## EDA Tools

### R

통계와 데이터 분석이 묶여 주로 사용되는 언어는 R이고, R에서는 ggplot이란 시각화 패키지를 사용할 수 있다. Tidy 문법에 기반해 그래프를 직관적으로 쌓아 나갈 수 있게 해주는 툴이다

R에서 interactive visualization은 R shiny라는 앱 구축 언어를 통해 구현할 수 있다.

### Python

 가장 기초적인 matplotlib 부터, seaborn, plotly, bokeh 등 파이썬에는 시각화 도구가 매우 다양하게 구축되어있다. R의 ggplot을 파이썬에서도 사용 가능하게 구현해 놓은 plotnine 또한 존재한다. 만일 정교한 시각화가 필요없다면 pandas-profiling 패키지를 사용하면 모든 열에 대한 정보를 모두 파악해준다.  
 interactive visualization을 원한다면 plotly, bokeh를 사용하면 된다

# Package


```python
import pandas as pd
import numpy as np
from plotnine import *
%matplotlib inline
```


```python
import shapefile
```

# Data

## CASE


```python
Case.head()
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
      <th>case_id</th>
      <th>province</th>
      <th>city</th>
      <th>group</th>
      <th>infection_case</th>
      <th>confirmed</th>
      <th>latitude</th>
      <th>longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000001</td>
      <td>Seoul</td>
      <td>Yongsan-gu</td>
      <td>True</td>
      <td>Itaewon Clubs</td>
      <td>139</td>
      <td>37.538621</td>
      <td>126.992652</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000002</td>
      <td>Seoul</td>
      <td>Gwanak-gu</td>
      <td>True</td>
      <td>Richway</td>
      <td>119</td>
      <td>37.48208</td>
      <td>126.901384</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000003</td>
      <td>Seoul</td>
      <td>Guro-gu</td>
      <td>True</td>
      <td>Guro-gu Call Center</td>
      <td>95</td>
      <td>37.508163</td>
      <td>126.884387</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000004</td>
      <td>Seoul</td>
      <td>Yangcheon-gu</td>
      <td>True</td>
      <td>Yangcheon Table Tennis Club</td>
      <td>43</td>
      <td>37.546061</td>
      <td>126.874209</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000005</td>
      <td>Seoul</td>
      <td>Dobong-gu</td>
      <td>True</td>
      <td>Day Care Center</td>
      <td>43</td>
      <td>37.679422</td>
      <td>127.044374</td>
    </tr>
  </tbody>
</table>
</div>



### Data Type


```python
# 174row가 있는데, 이 중 범주형은 Province, City, Group Infection, Infection_Case. geo-metric은 lat과 long
```

### Missing Value


```python
# 이런건 채울 수가 없긴 하겠지..
Case[Case.city == '-'].head()
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
      <th>case_id</th>
      <th>province</th>
      <th>city</th>
      <th>group</th>
      <th>infection_case</th>
      <th>confirmed</th>
      <th>latitude</th>
      <th>longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33</th>
      <td>1000034</td>
      <td>Seoul</td>
      <td>-</td>
      <td>True</td>
      <td>Orange Life</td>
      <td>1</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1000036</td>
      <td>Seoul</td>
      <td>-</td>
      <td>False</td>
      <td>overseas inflow</td>
      <td>298</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1000037</td>
      <td>Seoul</td>
      <td>-</td>
      <td>False</td>
      <td>contact with patient</td>
      <td>162</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <th>37</th>
      <td>1000038</td>
      <td>Seoul</td>
      <td>-</td>
      <td>False</td>
      <td>etc</td>
      <td>100</td>
      <td>-</td>
      <td>-</td>
    </tr>
    <tr>
      <th>45</th>
      <td>1100008</td>
      <td>Busan</td>
      <td>-</td>
      <td>False</td>
      <td>overseas inflow</td>
      <td>36</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>
</div>



### Group Infection by Case


```python
(
    ggplot(Case) 
    + geom_bar(aes(x='province', fill = 'group'))
    + ggtitle("Group Infection and Province by Case")
    + theme(axis_text_x=element_text(rotation=315, hjust=0))
)
#서울, 경기 등 인구가 많은 곳일수록 집단 감염으로 이루어짐을 알 수 있다.
```


![png](/images/COVID19_git_files/COVID19_git_33_0.png)





    <ggplot: (8729948200368)>




```python
top10case = Case.infection_case.value_counts()[1:11].index.tolist()
top10Case = Case[[x in top10case for x in Case.infection_case]]
```


```python
(
    ggplot(top10Case) 
    + geom_bar(aes(x='infection_case', fill='group'))
    + ggtitle("top 10 case")
    + theme(axis_text_x=element_text(rotation=315, hjust=0))
)
# 해외 유입 감염, 환자와 접촉 등 대비가 가능한 경우 집단 감염으로 이루어진 경우는 한 건도 없었다.
# 방역이 매우 잘 이루어지고 있음을 확인할 수 있다. 
```


![png](/images/COVID19_git_files/COVID19_git_35_0.png)





    <ggplot: (-9223363306906622341)>



### Grouped for num of Infection


```python
Case['confirmed'].groupby(Case['infection_case']).sum().head()
```




    infection_case
    Anyang Gunpo Pastors Group         23
    Biblical Language study meeting     3
    Bonghwa Pureun Nursing Home        68
    Bundang Jesaeng Hospital           22
    Changnyeong Coin Karaoke            7
    Name: confirmed, dtype: int64




```python
groupedCase = pd.DataFrame(Case.groupby(['infection_case',  'group', 'province'])['confirmed'].sum()).reset_index()
groupedCase.nlargest(20, 'confirmed').head()
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
      <th>infection_case</th>
      <th>group</th>
      <th>province</th>
      <th>confirmed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>93</th>
      <td>Shincheonji Church</td>
      <td>True</td>
      <td>Daegu</td>
      <td>4511</td>
    </tr>
    <tr>
      <th>125</th>
      <td>contact with patient</td>
      <td>False</td>
      <td>Daegu</td>
      <td>917</td>
    </tr>
    <tr>
      <th>141</th>
      <td>etc</td>
      <td>False</td>
      <td>Daegu</td>
      <td>747</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Shincheonji Church</td>
      <td>True</td>
      <td>Gyeongsangbuk-do</td>
      <td>566</td>
    </tr>
    <tr>
      <th>164</th>
      <td>overseas inflow</td>
      <td>False</td>
      <td>Gyeonggi-do</td>
      <td>305</td>
    </tr>
  </tbody>
</table>
</div>




```python
(
    ggplot(groupedCase.nlargest(10, 'confirmed')) 
    + geom_bar(aes(x='infection_case', y='confirmed', fill = 'province'),position='dodge' ,stat="identity")
    + ggtitle("grouped for num of Infection")
    + theme(axis_text_x=element_text(rotation=315, hjust=0))
)
```


![png](/images/COVID19_git_files/COVID19_git_39_0.png)





    <ggplot: (8770893301098)>



## PatientInfo


```python
PatientInfo.head()
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
      <th>patient_id</th>
      <th>sex</th>
      <th>age</th>
      <th>country</th>
      <th>province</th>
      <th>city</th>
      <th>infection_case</th>
      <th>infected_by</th>
      <th>contact_number</th>
      <th>symptom_onset_date</th>
      <th>confirmed_date</th>
      <th>released_date</th>
      <th>deceased_date</th>
      <th>state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000000001</td>
      <td>male</td>
      <td>50s</td>
      <td>Korea</td>
      <td>Seoul</td>
      <td>Gangseo-gu</td>
      <td>overseas inflow</td>
      <td>NaN</td>
      <td>75</td>
      <td>2020-01-22</td>
      <td>2020-01-23</td>
      <td>2020-02-05</td>
      <td>NaN</td>
      <td>released</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000000002</td>
      <td>male</td>
      <td>30s</td>
      <td>Korea</td>
      <td>Seoul</td>
      <td>Jungnang-gu</td>
      <td>overseas inflow</td>
      <td>NaN</td>
      <td>31</td>
      <td>NaN</td>
      <td>2020-01-30</td>
      <td>2020-03-02</td>
      <td>NaN</td>
      <td>released</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000000003</td>
      <td>male</td>
      <td>50s</td>
      <td>Korea</td>
      <td>Seoul</td>
      <td>Jongno-gu</td>
      <td>contact with patient</td>
      <td>2002000001</td>
      <td>17</td>
      <td>NaN</td>
      <td>2020-01-30</td>
      <td>2020-02-19</td>
      <td>NaN</td>
      <td>released</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000000004</td>
      <td>male</td>
      <td>20s</td>
      <td>Korea</td>
      <td>Seoul</td>
      <td>Mapo-gu</td>
      <td>overseas inflow</td>
      <td>NaN</td>
      <td>9</td>
      <td>2020-01-26</td>
      <td>2020-01-30</td>
      <td>2020-02-15</td>
      <td>NaN</td>
      <td>released</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000000005</td>
      <td>female</td>
      <td>20s</td>
      <td>Korea</td>
      <td>Seoul</td>
      <td>Seongbuk-gu</td>
      <td>contact with patient</td>
      <td>1000000002</td>
      <td>2</td>
      <td>NaN</td>
      <td>2020-01-31</td>
      <td>2020-02-24</td>
      <td>NaN</td>
      <td>released</td>
    </tr>
  </tbody>
</table>
</div>




```python
PatientInfoSeoul = PatientInfo[(PatientInfo.province == 'Seoul') & (PatientInfo.city!='etc')]
```


```python
PatientCounts = pd.DataFrame(PatientInfoSeoul.city.value_counts())
```

## Policy


```python
Policy.head()
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
      <th>policy_id</th>
      <th>country</th>
      <th>type</th>
      <th>gov_policy</th>
      <th>detail</th>
      <th>start_date</th>
      <th>end_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Korea</td>
      <td>Alert</td>
      <td>Infectious Disease Alert Level</td>
      <td>Level 1 (Blue)</td>
      <td>2020-01-03</td>
      <td>2020-01-19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Korea</td>
      <td>Alert</td>
      <td>Infectious Disease Alert Level</td>
      <td>Level 2 (Yellow)</td>
      <td>2020-01-20</td>
      <td>2020-01-27</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Korea</td>
      <td>Alert</td>
      <td>Infectious Disease Alert Level</td>
      <td>Level 3 (Orange)</td>
      <td>2020-01-28</td>
      <td>2020-02-22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Korea</td>
      <td>Alert</td>
      <td>Infectious Disease Alert Level</td>
      <td>Level 4 (Red)</td>
      <td>2020-02-23</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Korea</td>
      <td>Immigration</td>
      <td>Special Immigration Procedure</td>
      <td>from China</td>
      <td>2020-02-04</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## Region


```python
Region.head()
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
      <th>code</th>
      <th>province</th>
      <th>city</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>elementary_school_count</th>
      <th>kindergarten_count</th>
      <th>university_count</th>
      <th>academy_ratio</th>
      <th>elderly_population_ratio</th>
      <th>elderly_alone_ratio</th>
      <th>nursing_home_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10000</td>
      <td>Seoul</td>
      <td>Seoul</td>
      <td>37.566953</td>
      <td>126.977977</td>
      <td>607</td>
      <td>830</td>
      <td>48</td>
      <td>1.44</td>
      <td>15.38</td>
      <td>5.8</td>
      <td>22739</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10010</td>
      <td>Seoul</td>
      <td>Gangnam-gu</td>
      <td>37.518421</td>
      <td>127.047222</td>
      <td>33</td>
      <td>38</td>
      <td>0</td>
      <td>4.18</td>
      <td>13.17</td>
      <td>4.3</td>
      <td>3088</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10020</td>
      <td>Seoul</td>
      <td>Gangdong-gu</td>
      <td>37.530492</td>
      <td>127.123837</td>
      <td>27</td>
      <td>32</td>
      <td>0</td>
      <td>1.54</td>
      <td>14.55</td>
      <td>5.4</td>
      <td>1023</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10030</td>
      <td>Seoul</td>
      <td>Gangbuk-gu</td>
      <td>37.639938</td>
      <td>127.025508</td>
      <td>14</td>
      <td>21</td>
      <td>0</td>
      <td>0.67</td>
      <td>19.49</td>
      <td>8.5</td>
      <td>628</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10040</td>
      <td>Seoul</td>
      <td>Gangseo-gu</td>
      <td>37.551166</td>
      <td>126.849506</td>
      <td>36</td>
      <td>56</td>
      <td>1</td>
      <td>1.17</td>
      <td>14.39</td>
      <td>5.7</td>
      <td>1080</td>
    </tr>
  </tbody>
</table>
</div>




```python
SeoulInfo = Region[(Region.province=='Seoul') & (Region.city!='Seoul')]
SeoulInfo.columns = ['code', 'province', 'SIG_ENG_NM', 'latitude', 'longitude',
       'elementary_school_count', 'kindergarten_count', 'university_count',
       'academy_ratio', 'elderly_population_ratio', 'elderly_alone_ratio',
       'nursing_home_count']
```


```python
SeoulInfo = SeoulInfo.join(PatientCounts, on='SIG_ENG_NM')
SeoulInfo.columns = ['code', 'province', 'SIG_ENG_NM', 'latitude', 'longitude',
       'elementary_school_count', 'kindergarten_count', 'university_count',
       'academy_ratio', 'elderly_population_ratio', 'elderly_alone_ratio',
       'nursing_home_count', 'patient']
```

### 지도그리기


```python
def read_shapefile(shp_path):

    import shapefile

    #read file, parse out the records and shapes
    sf = shapefile.Reader(shp_path, encoding='cp949')
    fields = [x[0] for x in sf.fields][1:]
    records = sf.records()
    shps = [s.points for s in sf.shapes()]

    #write into a dataframe
    df = pd.DataFrame(columns=fields, data=records)
    df = df.assign(coords=shps)

    return df
```


```python
def lat(x):
    return x[0]

def lon(x):
    return x[1]
```


```python
sfdf = (
sfdf.coords.apply(lambda x: pd.Series(x))
        .stack()
        .reset_index(level=1, drop=True)
        .to_frame('coords')
        .join(sfdf[['SIG_CD', 'SIG_ENG_NM', 'SIG_KOR_NM']], how='left')
)
```


```python
sfdf = sfdf.reset_index(drop=True)
sfdf['lat'] = sfdf.coords.apply(lat)
sfdf['lon'] = sfdf.coords.apply(lon)
sfdf = sfdf[['SIG_CD', 'SIG_ENG_NM', 'SIG_KOR_NM', 'lat', 'lon']]
```


```python
sfdf.head()
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
      <th>SIG_CD</th>
      <th>SIG_ENG_NM</th>
      <th>SIG_KOR_NM</th>
      <th>coords</th>
      <th>lat</th>
      <th>lon</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11110</td>
      <td>Jongno-gu</td>
      <td>종로구</td>
      <td>[(956615.4532424484, 1953567.1989686124), (956...</td>
      <td>954424.008602</td>
      <td>1.953943e+06</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11140</td>
      <td>Jung-gu</td>
      <td>중구</td>
      <td>[(957890.3856818088, 1952616.7455681711), (957...</td>
      <td>954939.506510</td>
      <td>1.951513e+06</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11170</td>
      <td>Yongsan-gu</td>
      <td>용산구</td>
      <td>[(953115.7610894071, 1950834.083634671), (9531...</td>
      <td>953695.247727</td>
      <td>1.948812e+06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11200</td>
      <td>Seongdong-gu</td>
      <td>성동구</td>
      <td>[(959681.109391748, 1952649.6047979225), (9598...</td>
      <td>958183.469452</td>
      <td>1.950823e+06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11215</td>
      <td>Gwangjin-gu</td>
      <td>광진구</td>
      <td>[(964825.0579498123, 1952633.2496245715), (964...</td>
      <td>964073.061416</td>
      <td>1.950255e+06</td>
    </tr>
  </tbody>
</table>
</div>




```python
seoul_map = sfdf[sfdf.SIG_CD <= '11740']
seoul_map = seoul_map.join(PatientCounts, on='SIG_ENG_NM')
```


```python
gu_name = gu_name[gu_name.SIG_CD <= '11740']
gu_name = gu_name.join(PatientCounts, on='SIG_ENG_NM')
```


```python
(
ggplot() 
    + geom_polygon(aes(x='lat', y='lon', group='SIG_CD', fill='city'), data=seoul_map)
    + scale_fill_gradient(low = "#FBCF61",
                      high = "crimson") 
    + labs(fill = "Num of COVID-19 Patient")
    + theme_void()
    + theme(figure_size=(12,9), legend_position = (0.3, 0.7), legend_direction='horizontal',legend_key_width=10,
    legend_key_height=15)
    + geom_text(aes(x = 'lat', y = 'lon', label = 'SIG_ENG_NM'),data=gu_name)
    + geom_text(aes(x = 'lat', y = 'lon', label = 'city'),data=gu_name, format_string='\n\n {:}')
)
#plotnine과 shapefile을 활용해 지도를 구현할 수 있다
```


![png](/images/COVID19_git_files/COVID19_git_58_0.png)





    <ggplot: (8770880806783)>




```python
(
ggplot(SeoulInfo)
    +geom_point(aes(x = 'elementary_school_count', y = 'patient', fill='SIG_ENG_NM'), size=5)
)
#인구수와 correlation이 높아서 나온듯하다. 그 외 변수들은 큰 연관성을 보이지 못했다.
```


![png](/images/COVID19_git_files/COVID19_git_59_0.png)





    <ggplot: (-9223363266017760154)>



## SeoulFloating


```python
SeoulFloating
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
      <th>date</th>
      <th>hour</th>
      <th>birth_year</th>
      <th>sex</th>
      <th>province</th>
      <th>city</th>
      <th>fp_num</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-01</td>
      <td>0</td>
      <td>20</td>
      <td>female</td>
      <td>Seoul</td>
      <td>Dobong-gu</td>
      <td>19140</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-01</td>
      <td>0</td>
      <td>20</td>
      <td>male</td>
      <td>Seoul</td>
      <td>Dobong-gu</td>
      <td>19950</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-01</td>
      <td>0</td>
      <td>20</td>
      <td>female</td>
      <td>Seoul</td>
      <td>Dongdaemun-gu</td>
      <td>25450</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-01</td>
      <td>0</td>
      <td>20</td>
      <td>male</td>
      <td>Seoul</td>
      <td>Dongdaemun-gu</td>
      <td>27050</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-01</td>
      <td>0</td>
      <td>20</td>
      <td>female</td>
      <td>Seoul</td>
      <td>Dongjag-gu</td>
      <td>28880</td>
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
    </tr>
    <tr>
      <th>1084795</th>
      <td>2020-05-31</td>
      <td>21</td>
      <td>40</td>
      <td>female</td>
      <td>Seoul</td>
      <td>Dobong-gu</td>
      <td>27620</td>
    </tr>
    <tr>
      <th>1084796</th>
      <td>2020-05-31</td>
      <td>21</td>
      <td>40</td>
      <td>female</td>
      <td>Seoul</td>
      <td>Songpa-gu</td>
      <td>56560</td>
    </tr>
    <tr>
      <th>1084797</th>
      <td>2020-05-31</td>
      <td>21</td>
      <td>50</td>
      <td>female</td>
      <td>Seoul</td>
      <td>Gangdong-gu</td>
      <td>38960</td>
    </tr>
    <tr>
      <th>1084798</th>
      <td>2020-05-31</td>
      <td>22</td>
      <td>60</td>
      <td>female</td>
      <td>Seoul</td>
      <td>Guro-gu</td>
      <td>25420</td>
    </tr>
    <tr>
      <th>1084799</th>
      <td>2020-05-31</td>
      <td>23</td>
      <td>40</td>
      <td>male</td>
      <td>Seoul</td>
      <td>Eunpyeong-gu</td>
      <td>38650</td>
    </tr>
  </tbody>
</table>
<p>1084800 rows × 7 columns</p>
</div>



## Time


```python
Time.head()
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
      <th>date</th>
      <th>time</th>
      <th>test</th>
      <th>negative</th>
      <th>confirmed</th>
      <th>released</th>
      <th>deceased</th>
      <th>datetime</th>
      <th>dailyConfirmed</th>
      <th>dialyTested</th>
      <th>confirmedRatio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-20</td>
      <td>16</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2020-01-20</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-21</td>
      <td>16</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2020-01-21</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-22</td>
      <td>16</td>
      <td>4</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2020-01-22</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-23</td>
      <td>16</td>
      <td>22</td>
      <td>21</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2020-01-23</td>
      <td>0.0</td>
      <td>18.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-24</td>
      <td>16</td>
      <td>27</td>
      <td>25</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2020-01-24</td>
      <td>1.0</td>
      <td>5.0</td>
      <td>0.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
Time['datetime'] = Time.date.apply(lambda x: datetime.datetime.strptime(x, '%Y-%m-%d'))
```


```python
dailyConfirmed = Time.confirmed - Time.confirmed.shift()
dailyConfirmed[0] = 1
```


```python
dailyTested = Time.test - Time.test.shift()
dailyTested[0] = 1
```


```python
Time['dailyConfirmed'] = dailyConfirmed
Time['dialyTested'] = dailyTested
```


```python
Time = Time.assign(confirmedRatio= lambda x: x['dailyConfirmed'] / x['dialyTested'])
```


```python
(
    ggplot(data = Time) 
    + geom_line(mapping=aes(x='datetime', y='confirmedRatio',  group=1))
    + ylim(0,0.3)
    + ggtitle("Ratio of confirmed")

)
# 코로나19에 대한 한국의 공격적 진단의 실태를 확인할 수 있다.
```

    /home/lds/anaconda3/envs/DL/lib/python3.7/site-packages/plotnine/geoms/geom_path.py:75: PlotnineWarning: geom_path: Removed 2 rows containing missing values.



![png](/images/COVID19_git_files/COVID19_git_69_1.png)





    <ggplot: (8770836114496)>



## TimeAge


```python
import datetime
```


```python
TimeAge
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
      <th>date</th>
      <th>time</th>
      <th>age</th>
      <th>confirmed</th>
      <th>deceased</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-03-02</td>
      <td>0</td>
      <td>0s</td>
      <td>32</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-03-02</td>
      <td>0</td>
      <td>10s</td>
      <td>169</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-03-02</td>
      <td>0</td>
      <td>20s</td>
      <td>1235</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-03-02</td>
      <td>0</td>
      <td>30s</td>
      <td>506</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-03-02</td>
      <td>0</td>
      <td>40s</td>
      <td>633</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1084</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>40s</td>
      <td>1681</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1085</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>50s</td>
      <td>2286</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1086</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>60s</td>
      <td>1668</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1087</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>70s</td>
      <td>850</td>
      <td>82</td>
    </tr>
    <tr>
      <th>1088</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>80s</td>
      <td>556</td>
      <td>139</td>
    </tr>
  </tbody>
</table>
<p>1089 rows × 5 columns</p>
</div>




```python
TimeAge['datetime'] = TimeAge.date.apply(lambda x: datetime.datetime.strptime(x, '%Y-%m-%d'))
```


```python
TimeAge[TimeAge.date=='2020-06-30'].nlargest(11, 'confirmed').age.tolist()
```




    ['20s', '50s', '40s', '60s', '30s', '70s', '10s', '80s', '0s']




```python
label = TimeAge[TimeAge.date=='2020-06-30'].nlargest(11, 'confirmed').age.tolist()
(
    ggplot(data = TimeAge) 
    + geom_line(mapping=aes(x='datetime', y='confirmed', group='age', color='age'))
    + scale_color_discrete(limits=label)
    + ggtitle("TimeAge of confirmed")
    + theme(axis_text_x=element_text(rotation=315))

)
# 20대와 50대에서 가장 많은 확진자가 나왔음을 확인할 수 있다.

```


![png](/images/COVID19_git_files/COVID19_git_75_0.png)





    <ggplot: (8770836117203)>




```python
label = TimeAge[TimeAge.date=='2020-06-30'].nlargest(11, 'deceased').age.tolist()
(
    ggplot(data = TimeAge) 
    +geom_line(aes(x='datetime', y='deceased', group='age', color='age'))
    + scale_color_discrete(limits=label)
    + ggtitle("TimeAge of deceased")
    + theme(axis_text_x=element_text(rotation=315))

)
# 하지만 반면 사망자 수는 확실히 고연령에서 높게 나타남을 볼 수 있다.
```


![png](/images/COVID19_git_files/COVID19_git_76_0.png)





    <ggplot: (-9223363266018014762)>



## TimeGender


```python
TimeGender
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
      <th>date</th>
      <th>time</th>
      <th>sex</th>
      <th>confirmed</th>
      <th>deceased</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-03-02</td>
      <td>0</td>
      <td>male</td>
      <td>1591</td>
      <td>13</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-03-02</td>
      <td>0</td>
      <td>female</td>
      <td>2621</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-03-03</td>
      <td>0</td>
      <td>male</td>
      <td>1810</td>
      <td>16</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-03-03</td>
      <td>0</td>
      <td>female</td>
      <td>3002</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-03-04</td>
      <td>0</td>
      <td>male</td>
      <td>1996</td>
      <td>20</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>237</th>
      <td>2020-06-28</td>
      <td>0</td>
      <td>female</td>
      <td>7265</td>
      <td>131</td>
    </tr>
    <tr>
      <th>238</th>
      <td>2020-06-29</td>
      <td>0</td>
      <td>male</td>
      <td>5470</td>
      <td>151</td>
    </tr>
    <tr>
      <th>239</th>
      <td>2020-06-29</td>
      <td>0</td>
      <td>female</td>
      <td>7287</td>
      <td>131</td>
    </tr>
    <tr>
      <th>240</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>male</td>
      <td>5495</td>
      <td>151</td>
    </tr>
    <tr>
      <th>241</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>female</td>
      <td>7305</td>
      <td>131</td>
    </tr>
  </tbody>
</table>
<p>242 rows × 5 columns</p>
</div>




```python
TimeGender['datetime'] = TimeGender.date.apply(lambda x: datetime.datetime.strptime(x, '%Y-%m-%d'))
```


```python
dailyConfirmed = TimeGender.confirmed - TimeGender.confirmed.shift(2)
dailyConfirmed[:2] = TimeGender.confirmed[:2]
TimeGender['dailyConfirmed'] = dailyConfirmed
```


```python
(
    ggplot(data = TimeGender) 
    +geom_line(aes(x='datetime', y='dailyConfirmed', group='sex', color='sex'))
    + ggtitle("confirmed by sex")
    + theme(axis_text_x=element_text(rotation=315))
    + ylim(0,400)

)
#남자가 코로나 바이러스에 덜 감염된다고 알려져 있으나, 방역이 잘 되고 있는 상황에서는, 감염에 있어 성별에 따른 차이가 존재한다고 보기 힘들다.
```

    /home/lds/anaconda3/envs/DL/lib/python3.7/site-packages/plotnine/geoms/geom_path.py:75: PlotnineWarning: geom_path: Removed 1 rows containing missing values.



![png](/images/COVID19_git_files/COVID19_git_81_1.png)





    <ggplot: (8770891307023)>



## TimeProvince


```python
TimeProvince
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
      <th>date</th>
      <th>time</th>
      <th>province</th>
      <th>confirmed</th>
      <th>released</th>
      <th>deceased</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-01-20</td>
      <td>16</td>
      <td>Seoul</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-01-20</td>
      <td>16</td>
      <td>Busan</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-01-20</td>
      <td>16</td>
      <td>Daegu</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-01-20</td>
      <td>16</td>
      <td>Incheon</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-01-20</td>
      <td>16</td>
      <td>Gwangju</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2766</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>Jeollabuk-do</td>
      <td>27</td>
      <td>21</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2767</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>Jeollanam-do</td>
      <td>24</td>
      <td>19</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2768</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>Gyeongsangbuk-do</td>
      <td>1389</td>
      <td>1328</td>
      <td>54</td>
    </tr>
    <tr>
      <th>2769</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>Gyeongsangnam-do</td>
      <td>134</td>
      <td>128</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2770</th>
      <td>2020-06-30</td>
      <td>0</td>
      <td>Jeju-do</td>
      <td>19</td>
      <td>16</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>2771 rows × 6 columns</p>
</div>




```python
TimeProvince['datetime'] = TimeProvince.date.apply(lambda x: datetime.datetime.strptime(x, '%Y-%m-%d'))
```


```python
dailyConfirmed = TimeProvince.confirmed - TimeProvince.confirmed.shift(17)
dailyConfirmed[:17] = TimeProvince.confirmed[:17]
TimeProvince['dailyConfirmed'] = dailyConfirmed
```


```python
(
    ggplot(data = TimeProvince) 
    +geom_line(aes(x='datetime', y='dailyConfirmed', group='province', color='province'))
#    + geom_line(mapping=aes(x='date', y='confirmed', group='age', color='age'))
    + ggtitle("TimeProvince of confirmed")
    + theme(axis_text_x=element_text(rotation=315))

)
# 데이터프레임을 바꾸거나, geom_line을 바꾸거나

```


![png](/images/COVID19_git_files/COVID19_git_86_0.png)





    <ggplot: (-9223363265960634182)>




```python
(
    ggplot(data = TimeProvince) 
    +geom_line(aes(x='datetime', y='dailyConfirmed', group='province', color='province'))
    + ggtitle("TimeProvince of confirmed")
    + theme(axis_text_x=element_text(rotation=315))
    + facet_wrap('province', ncol = 3)
    + scale_color_discrete(guide=False)

)
# facet을 통해 그룹별로 나누어 그래프를 그릴 수 있다.

```


![png](/images/COVID19_git_files/COVID19_git_87_0.png)





    <ggplot: (-9223363265964993322)>



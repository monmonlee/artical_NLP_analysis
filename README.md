# artical_NLP_analysis
##### I've utilized BigQuery to acquire raw data on the top 20 scoring keywords from 20 articles across 27 channels. This raw data includes the article name, article views, article ID (PID), and the keywords. The aim is to use these keywords to describe the target audience. This is achieved by calculating the significance of each keyword, taking into account both the frequency of the keyword's appearance and its order in each row as weighting factors.

#### 1. reading xlsx file
```{reading xlsx file}
import pandas as pd
from collections import Counter
df = pd.read_excel(r'C:\Users\40050\Desktop\pets_nlp.xlsx')
```

#### 2. cleaning keywords data
##### "keywords" column schema look like this:
[風格,月曆,皮件,萬寶龍,倒數,白朗峰,文具,朋友,相約,到貨,聚會,皮夾,台灣,幾何,圖形,排比,ArtDeco,後背包,圖案,油光]


```{cleaning keywords data}
df['keywords'] = df['keywords'].str.replace('[', '', regex=False)
df['keywords'] = df['keywords'].str.replace(']', '', regex=False)
df['keywords']
```
outputs:
```
0      惜物祭,物品,印良品,空氣,價格,顧客,收納箱,冠軍,商品,全台門市,MUJI,門市,好評,...
1      品牌,空間,設計,旗艦店,餐廳,運動,概念,冰場,時尚,專門店,隈研吾,國際,風格,選品,商...
2      總館,圖書館,空間,知識,基地,設計,環境,採光井,書架,文化,圓錐狀,概念,綠色,生命樹,...
3      奈良美智,作品,台灣,美術館,山子,旅行,旅程,特展,期間,畫作,巡迴...
```

#### 3. scoring every keyword by order weight and articles' views

```
word_freq = Counter()

# 遍歷每一行資料
for _, row in df.iterrows():
    weight = 20  # assume the most impartant keyword weight is 20
    
    # use split() to convert keyword from str to list
    keywords = row['keywords'].split(',')
    
    for word in keywords:
        word_freq[word] += weight * row['n']  # aggregate the product of views and weight
        weight -= 1  # decrease the weight of next keywords 
```

#### 4. convert results into DataFrame and export to Excel"

```
#convert Counter into list of tuples

keyword_scores = list(word_freq.items())

# convert into DataFrame
df = pd.DataFrame(keyword_scores, columns=['Keyword', 'Score'])

# write to excel
df.to_excel('keyword_scores.xlsx', index=False)
```

#### the results

```
Keyword	Score
網友	8391226 
台灣	2690584 
影片	2129548 
PO	1852062 
日本	1849386 
貼文	1728313 
照片	1723648 
兒子	1669180 
美國	1543638 
男子	1483877 
民眾	1460821 
學生	1189131 
大陸	1163518 
.
.
.

```







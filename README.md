# artical_NLP_analysis
#### I've utilized BigQuery to acquire raw data on the top 20 scoring keywords from 20 articles across 27 channels. This raw data includes the article name, article views, article ID (PID), and the keywords. The aim is to use these keywords to describe the target audience. This is achieved by calculating the significance of each keyword, taking into account both the frequency of the keyword's appearance and its order in each row as weighting factors.

#### reading xlsx file
```{reading xlsx file}
import pandas as pd
from collections import Counter
df = pd.read_excel(r'C:\Users\40050\Desktop\pets_nlp.xlsx')
```

#### cleaning keywords data
##### "keywords" column schema look like this:

###### [風格,月曆,皮件,萬寶龍,倒數,白朗峰,文具,朋友,相約,到貨,聚會,皮夾,台灣,幾何,圖形,排比,ArtDeco,後背包,圖案,油光]


```{cleaning keywords data}
df['keywords'] = df['keywords'].str.replace('[', '', regex=False)
df['keywords'] = df['keywords'].str.replace(']', '', regex=False)
df['keywords']
```

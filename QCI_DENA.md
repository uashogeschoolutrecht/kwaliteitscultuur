# Kwaliteitscultuur

# QCI

#### Author: Jan T. (IR) en Team D&A

``` python
###Load packages
import pandas       as pd   #required for data wrangling
import pingouin     as pg   #required for Cronbach's Alpha
import numpy        as np   #required for NaN
```

``` python
### Load data
# Use sample data because of unavailability of QCI data
qcidata = pd.DataFrame({   'Vraag3': [3, 2, 2, 3, 2, 2, 3, 3, 6, 1],
                            'Vraag4': [1, 1, 1, 2, 3, 3, 2, 3, 3, 3],
                            'Vraag5': [1, 0, 2, 1, 2, 3, 3, 3, 2, 3],
                            'Vraag6': [3, 2, 2, 3, 2, 2, 3, 3, 6, 1],
                            'Vraag7': [1, 1, 1, 2, 3, 3, 2, 3, 3, 3],
                            'Vraag8': [1, 1, 2, 1, 2, 3, 3, 3, 2, 3],
                            'Vraag9': [1, 1, 2, 1, 2, 3, 3, 3, 2, 8]})
(
    qcidata.style # Needed to convert df.head() to kbl format
    .hide(axis='index')
)
```

TABLE 1. Sample data.

| Vraag3 | Vraag4 | Vraag5 | Vraag6 | Vraag7 | Vraag8 | Vraag9 |
|--------|--------|--------|--------|--------|--------|--------|
| 3      | 1      | 1      | 3      | 1      | 1      | 1      |
| 2      | 1      | 0      | 2      | 1      | 1      | 1      |
| 2      | 1      | 2      | 2      | 1      | 2      | 2      |
| 3      | 2      | 1      | 3      | 2      | 1      | 1      |
| 2      | 3      | 2      | 2      | 3      | 2      | 2      |
| 2      | 3      | 3      | 2      | 3      | 3      | 3      |
| 3      | 2      | 3      | 3      | 2      | 3      | 3      |
| 3      | 3      | 3      | 3      | 3      | 3      | 3      |
| 6      | 3      | 2      | 6      | 3      | 2      | 2      |
| 1      | 3      | 3      | 1      | 3      | 3      | 8      |



## Data cleaning

Remove all values 0, 6, 7 and 8 (corresponding to some missing data
type), since they will influence the outcome. In this case, the best
method is to replace these values by ‘NaN’ (not a number).

``` python
missing_numbers = [0,6,7,8]
qcidata_clean = qcidata.replace(missing_numbers[0], np.NaN)
```

## Interne consistentie

Om interne consistentie per subschaal te meten is [Cronbach’s
Alpha](https://www.scribbr.nl/statistiek/cronbachs-alpha/) gebruikt,
deze is geïnterpreteerd met gebruik van de volgende
[bron](https://towardsdatascience.com/cronbachs-alpha-theory-and-application-in-python-d2915dd63586).

### Definieer subschalen

Elke subschaal bestaat uit een aantal vragen. Hier wordt voor elke
subschaal gedefinieerd uit welke vragen deze bestaat, en welke
subschalen er totaal zijn.

``` python
# Definieer vragen per subschalen
doeltreffendheid = ['Vraag3', 'Vraag4', 'Vraag5', 'Vraag6']
affectiviteit = ['Vraag7', 'Vraag8', 'Vraag9']

# Alle subschalen verzameld
subschalen = [doeltreffendheid, affectiviteit]
N_subschalen = len(subschalen)
```

``` python
# Definieer vragen per subschalen
alphas = []
for i in range(0,N_subschalen):
    alpha = (pg.cronbach_alpha(data=qcidata[subschalen[i]]))[0]
    alphas.append(alpha)
print(f'Aplhas: {alphas}')
```

    Aplhas: [0.6445366528354081, 0.7288629737609331]

``` python
alpha_threshold = 0.7
#test
```

``` python
# Padanalyse test
```

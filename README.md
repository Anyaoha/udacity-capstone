## 2016 POTUS US Primary Election Results 

#####  Run: [`analysis.ipynb`](https://github.com/Tsmith5151/2016-US-Election-ML/blob/master/analysis.ipynb)

### Data Description

- The 2016 US Election dataset contains several main files and folders.
  - primary_results.csv: main primary results file
  - state: state where the primary or caucus was held
  - state_abbreviation: two letter state abbreviation
  - county: county where the results come from
  - fips: FIPS county code
  - party: Democrat or Republican
  - candidate: name of the candidate
  - votes: number of votes the candidate received in the corresponding state and county (may be missing)
  - fraction_votes: fraction of votes the president received in the corresponding state, county, and primary

- Demographics:
  - county_facts.csv: demographic data on counties from US census
  - county_facts_dictionary.csv: description of the columns in county_facts
  - A complete description of the `county_facts` can be found [`here`](https://github.com/Tsmith5151/2016-US-Election-ML/blob/master/county_facts_dict.csv)

- SQL Database:
  - database.sqlite: SQLite database containing the primary_results, county_facts, and county_facts_dictionary tables with identical     data and schema

#### Libraries:
```python
import sys
import pandas as pd
#pd.set_option('display.max_rows', 1300)
import numpy as np
import matplotlib.pyplot as pl
import networkx as nx
import pygraphviz
import seaborn as sns
import sqlite3
import time
import pydot
import os
import time
from StringIO import StringIO
from io import BytesIO
from IPython.display import Image
%matplotlib inline 
```

#### Sci-Kit Learn:
``` python
from sklearn.metrics import confusion_matrix
from sklearn.decomposition import PCA
from sklearn import preprocessing
from sklearn.metrics import f1_score, accuracy_score
from sklearn.cross_validation import cross_val_score
from sklearn.cross_validation import StratifiedShuffleSplit
from sklearn.ensemble import RandomForestClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.svm import SVC
from sklearn.grid_search import GridSearchCV
from sklearn.metrics import classification_report
from sklearn import tree
from sklearn.externals.six import StringIO   
from sklearn.tree import export_graphviz
from sklearn.feature_extraction import DictVectorizer
```

  - To run `SQLITE3` in the `ipython notebook`kernel, install sql magic for IPython:
     ```python pip install ipython-sql```
  - Examples how to use ipython-sql can be foud [`here`](https://github.com/catherinedevlin/ipython-sql)

``` python
%load_ext sql
%sql sqlite:///database.sqlite
```
#### Data Source:
- (`Primary Results from CNN`)[http://www.cnn.com/election/primaries/counties/ia/Dem]
- (`New Hamphsire County-Level Results`)[https://numeracy.co/projects/2n9KPEk6ShS]
- (`County Facts`)[http://www.census.gov/quickfacts/404.php]


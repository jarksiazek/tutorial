### Creating Model ###

Prediction using decision tree
```python
import pandas as pd 
from sklearn.tree import DecisionTreeClassifier

df = pd.read_csv('misic.csv')
df.shape #numer of rows and columns
df.describe() #the most useful statistics
df.values() #chaning csv to array
X = df.drop(columns='genre')
y= df['genre']

model = DecisionTreeClassifier()
model.fit(X, y) #looking for algorithm

predictions = model.predict ([ [21, 1] ]) #looking for prediction 21 years, female

```

Prediction using decision tree - split model training test
```python
import pandas as pd 
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

df = pd.read_csv('misic.csv')
df.shape #numer of rows and columns
df.describe() #the most useful statistics
df.values() #chaning csv to array
X = df.drop(columns='genre')
y= df['genre']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = DecisionTreeClassifier()
model.fit(X_train, X_test) #looking for algorithm

predictions = model.predict (X_test) #looking for prediction 21 years, female

score = accuracy_score(y_test, predictions)
score
```

### Persist Model ###
Model persisting - saving training model results 
```python
import pandas as pd 
from sklearn.tree import DecisionTreeClassifier
from sklearn.externals import joblib

df = pd.read_csv('misic.csv')
X = df.drop(columns='genre')
y= df['genre']

model = DecisionTreeClassifier()
model.fit(X, y) 

joblib.dump(model, "storingFileName.joblib") #prediction results will be store in file 'storingFileName'
```
 
Model persisting - loading prediciton model 
```python
import pandas as pd 
from sklearn.tree import DecisionTreeClassifier
from sklearn.externals import joblib

model = joblib.load("storingFileName.joblib") #loading model from file 'storingFileName'

predictions = model.predict([[21, 1]])
```


Model persisting - loading prediciton model 
```python
import pandas as pd 
from sklearn.tree import DecisionTreeClassifier
from sklearn.externals import joblib

model = joblib.load("storingFileName.joblib") #loading model from file 'storingFileName'

predictions = model.predict([[21, 1]])
```

### Visual Decision Tree ###
```python
import pandas as pd 
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree

df = pd.read_csv('misic.csv')
X = df.drop(columns='genre')
y= df['genre']

model = DecisionTreeClassifier()
model.fit(X, y) 

tree.export_graphiz(model, out_file='music-recommender.dot', feature_names=['age', 'gender'],
                    class_names=sorted(y.unique()), label='all', rounded=True, filled=True)
```
# Modules #

app1.py
```python
def lbs_to_kg(weight):
    return weight * 0.45

def kg_to_lbs(weight):
    return weight / 0.45

```

app.py - import whole module 
```python
import app1

app1.lbs_to_kg(70)
```

app.py - import specific  module 
```python
from app1 import lbs_to_kg

lbs_to_kg(70)
```